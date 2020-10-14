---
layout: post
title: An API layer of PowerShell-based Function Apps - a few tips
tags: [pipelines]
---
Something that's really fascinating for me is how serverless brings new life to existing pieces of technology - in this case, Azure Function Apps. PowerShell-based ones in particular.

I am sure you are familiar with Function Apps and serverless computing, and the fact that amongst the various runtimes at your disposal you can even use PowerShell to write the logic inside them. When it comes to interacting with Azure and parsing files PowerShell is really second to none, and it makes our lives really easy. Embedding scripts (especially if they interact with an Azure estate) onto an Azure Function transforms them into a lightweight yet powerful API layer.

Once you start doing that, you will need a CI/CD process, and that's where things become interesting...

#### Getting started - CI/CD

First of all I would recommend **a repository per App Service Plan**.  
Azure Functions are simple, nimble pieces of code, and they are designed for being hosted on a single App Service Plan - so it makes sense to actually group them like this.

Once you have them there, add the ARM template or your favourite Infrastructure as Code equivalent. You need that so it's all reproducible!

Eventually, your CI/CD pipeline should have multiple stages - one for the infrastructure to be deploted or refreshed, and another one to deploy your Function(s).  

The deployment itself is the simplest thing ever: PowerShell doesn't need to be compiled, so you can just zip the code in a package file and push it via the relevant Pipelines task to Azure. All you need to do is to target your Function App, every Function will be loaded independently.

```
...
stages:
- stage: Infrastructure Deployment
  jobs:
  - deployment: TargetEnvironment
    environment:
      name: "My target environment"
    strategy:
        runOnce:
          deploy:
              steps:
                ...
- stage: Functions Package and Deployment
  jobs:
  - job: Package and Deployment
    steps:
    - task: ArchiveFiles@2
    inputs:
        rootFolderOrFile: '$(System.DefaultWorkingDirectory)'
        includeRootFolder: false
        archiveType: 'zip'
        archiveFile: '$(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip'
        replaceExistingArchive: true

    - task: PublishPipelineArtifact@1
    inputs:
        targetPath: '$(Build.ArtifactStagingDirectory)'
        artifact: 'Middleware'
        publishLocation: 'pipeline'
  
    - task: AzureFunctionApp@1
    inputs:
        azureSubscription: 'YourCSN'
        appType: 'functionApp'
        appName: 'YourFunctionApp'
        package: '$(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip'
        deploymentMethod: 'auto'
```

#### Should I group them?
The one above is just an example, but it gives you an idea. If you package everything in a single zip file, it will work fine. If you want granularity, you can have individual pipelines for individual functions, and as long as you target the Function App you are good to go.

#### Pair them with a Managed Identity for a managed and powerful API layer
You can easily add a Managed Identity to a Function App, and once the AAD Application Registration is secured you can leverage that to provide your users with self-service APIs spanning across your Azure estate.  

![](/images/posts/2020-10-14_20-24-17.png)

Remember that you have the full power of the Az commands in PowerShell, so everything you did up to today to automate tasks can be easily ported across. Putting that into an API gives it a whole different exposure.

#### Connect Azure Active Directory to secure the API layer
Integrating Azure Active Directory with your Function App is fairly simple, and it gives you control over who can access the API. Integration is straightforward, and it allows you to control access via RBAC.

![](/images/posts/2020-10-14_20-27-12.png)

It's all very powerful yet easy to setup and integrate, an extremely useful way of extending your automations and ensuring as many users as possible can benefit from them within your organisation.