---
layout: post
title: A primer on using VMs with multi-stage pipelines
tags: [pipeline]
---
One of the most demanded features for multi-stage pipelines in Azure DevOps is the possibility of natively targeting VMs. As of today you can easily target Kubernetes environments and cloud-hosted environments, but it is not yet possible to consume a set of targets made of virtual machines. Unfortunately we do not live in an ideal world where all the workloads are running in PaaS or containers, so at the moment we really cannot use it at scale with VMs. This changes with the new feature released last Friday: you will be able to target VMs directly as well as the above resources. How?

It's simple - the YAML syntax will have support for a new environment _resourceType_, called VirtualMachine. That one has got support for tagging and strategies designed around VMs.
The best part IMHO is that it is completely transparent: once you have it setup you can keep writing your pipelines exactly like you would with a K8S or a PaaS environment.

All you have to do is to create a new Environment with a _Virtual machine_ resource, specify the OS you are running and eventually run the associated script on your target VM. 

![](/images/posts/2019-12-19_19-22-01.png)

![](/images/posts/2019-12-19_19-22-39.png)

There you will be able to enter the resource tags you might want to use (in my case, simply _web_). As simple as any other Azure DevOps agent deployment.

![](/images/posts/2019-12-19_20-11-42.png)

It's all you have to do , once done you can start using your pipelines as usual. Let's take a simple example - a modernised version of the [PartsUnlimitedMRP](https://microsoft.github.io/PartsUnlimitedMRP/) sample app:

```
# Gradle
# Build your Java project and run tests with Gradle using a Gradle wrapper script.
# Add steps that analyze code, save build artifacts, deploy, and more:
# https://docs.microsoft.com/azure/devops/pipelines/languages/java

stages:
    - stage: Build
      jobs:
        - job: Build
          pool:
            vmImage: 'vs2017-win2016'
          steps:
          - task: Gradle@2
            displayName: 'Integration Service'
            inputs:
              workingDirectory: 'src/Backend/IntegrationService'
              gradleWrapperFile: 'src/Backend/IntegrationService/gradlew'
              gradleOptions: '-Xmx3072m'
              javaHomeOption: 'JDKVersion'
              jdkVersionOption: '1.8'
              jdkArchitectureOption: 'x64'
              publishJUnitResults: false
              testResultsFiles: '**/TEST-*.xml'
              tasks: 'build'

          - task: Gradle@2
            displayName: 'Order Service'
            inputs:
              workingDirectory: 'src/Backend/OrderService'
              gradleWrapperFile: 'src/Backend/OrderService/gradlew'
              gradleOptions: '-Xmx3072m'
              javaHomeOption: 'JDKVersion'
              jdkVersionOption: '1.8'
              jdkArchitectureOption: 'x64'
              publishJUnitResults: false
              testResultsFiles: '**/TEST-*.xml'
              tasks: 'build'

          - task: Gradle@2
            displayName: 'Clients'
            inputs:
              workingDirectory: 'src/Clients'
              gradleWrapperFile: 'src/Clients/gradlew'
              gradleOptions: '-Xmx3072m'
              javaHomeOption: 'JDKVersion'
              jdkVersionOption: '1.8'
              jdkArchitectureOption: 'x64'
              publishJUnitResults: false
              testResultsFiles: '**/TEST-*.xml'
              tasks: 'build'

          - task: CopyFiles@2
            displayName: 'Copy drop'
            inputs:
              SourceFolder: '$(Build.SourcesDirectory)\src'
              Contents: '**/build/libs/!(buildSrc)*.?ar'
              TargetFolder: '$(build.artifactstagingdirectory)\drop'

          - task: CopyFiles@2
            displayName: 'Copy deployment artifacts'
            inputs:
              SourceFolder: '$(Build.SourcesDirectory)'
              Contents: |
                **/deploy/SSH-MRP-Artifacts.ps1
                **/deploy/deploy_mrp_app.sh
                **/deploy/MongoRecords.js
              TargetFolder: '$(build.artifactstagingdirectory)\deploy'
            
          - task: PublishPipelineArtifact@1
            displayName: 'Upload drop'
            inputs:
              targetPath: '$(build.artifactstagingdirectory)\drop'
              artifact: 'drop'
              publishLocation: 'pipeline'

          - task: PublishPipelineArtifact@1
            displayName: 'Upload deploy'
            inputs:
              targetPath: '$(build.artifactstagingdirectory)\deploy'
              artifact: 'deploy'
              publishLocation: 'pipeline'
    
    - stage: Release
      jobs:
        - deployment: VMDeployment
          displayName: "Deployment on local Ubuntu VM"
          environment:
            name: "Target VMs"
            resourceType: VirtualMachine
            tags: web
          strategy:
              runOnce:
                  preDeploy:
                    steps:
                      - task: Bash@3
                        inputs:
                          targetType: 'inline'
                          script: 'echo ''Hello world'''
                  deploy:
                      steps:
                        - task: DownloadPipelineArtifact@2
                          inputs:
                            buildType: 'specific'
                            project: 'daf1bce1-923a-41af-ad31-cfebfd7eda61'
                            definition: '115'
                            buildVersionToDownload: 'latest'
                            artifactName: 'drop'
                            targetPath: '$(Pipeline.Workspace)'
                        - task: DownloadPipelineArtifact@2
                          inputs:
                            buildType: 'specific'
                            project: 'daf1bce1-923a-41af-ad31-cfebfd7eda61'
                            definition: '115'
                            buildVersionToDownload: 'latest'
                            artifactName: 'deploy'
                            targetPath: '$(Pipeline.Workspace)'
                        - task: Bash@3
                          inputs:
                            filePath: '$(Pipeline.Workspace)/deploy/deploy_mrp_app.sh'
```

The Build stage of my pipeline runs on a hosted agent: I am building the Java services with it. I don't have a Gradle build server easily available (nor I want to spend the effort of setting up one!), and as it is provided by Azure Pipelines it suits my requirement.
Once the Build stage is done, the Release starts. I am targeting the environment I created before (_Target VMs_), and I am pointing at all the VMs with the _web_ tag.

From there I am using one of the OOB strategies, called _runOnce_. As the name suggests, it runs once on all the targets, and it has two distinct phases: a preDeploy one, and a main phase for deployment.

The preDeploy phase allows to run specific tasks before the main deployment phase, and it is very useful for setting the environment before the actual deployment. In my case I am running a simple echo script, also because there used to be a bug where the runOnce strategy didn't run correctly without it. This has been fixed, but I left it out as an example.

In the main deploy phase the pipeline starts by explicitly downloading from a set of build artifacts. It could be the previous phase (it is in this case), but it could also be from other pipelines. It allows you to shape the pipeline in a granular way, effectively. Then it runs a script to deploy the MRP application (as it comes in the original codebase) via Bash. Again, as simple as we are used to.

The task support is exactly the same as the classic UI-based pipelines and the YAML pipelines. What I find extremely interesting is the OOB support for **Rolling** deployments, which I will cover in a separate post. Canary and Blue-Green will be implemented as well in the future.


