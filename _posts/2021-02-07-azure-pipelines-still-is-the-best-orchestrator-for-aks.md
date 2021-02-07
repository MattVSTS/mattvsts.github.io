---
layout: post
title: Why I believe Azure Pipelines is still the best orchestrator for Azure Kubernetes Services
tags: [pipelines, aks]
---
Small confession to make: I don't get excited by pure technology anymore.  

Gone are the _pioneeristic_ days of getting something together, as in 2021 we now have such a wealth of technologies, frameworks and documentation that makes it a degree of magnitude easier to do anything compared to even just five years ago.

Today I spent some time on a pet project of mine on Azure Kubernetes Services, and taking a step back from the code I just realised how much work happens behind the scenes and how easy Azure Pipelines makes it for any AKS user to not only setup the CI/CD process, but also to maintain extreme control while still having accelerators and automations doing things for you.

![](/images/posts/2021-02-06_20-40-30.png)

Once the Service Principal is configured with the appropriate permissions (in the real world you usually do :-) ) you can use the Service Connection anywhere within your YAML pipeline - that is extremely handy, and it also enables appropriate usage of Environments:

```yml
  jobs:
  - deployment: Deploy
    displayName: Deploy
    pool:
      vmImage: 'ubuntu-latest'
    environment: 'AKS'
    strategy:
      runOnce:
        deploy:
          steps:
          - task: KubernetesManifest@0
            displayName: Create imagePullSecret
            inputs:
              action: 'createSecret'
              kubernetesServiceConnection: 'dev-aks-default'
              namespace: 'default'
              secretType: 'dockerRegistry'
              secretName: '$(imagePullSecret)'
              dockerRegistryEndpoint: '$(dockerRegistryServiceConnection)'
              
          - task: KubernetesManifest@0
            displayName: Deploy to Kubernetes cluster
            inputs:
              action: 'deploy'
              kubernetesServiceConnection: 'dev-aks-default'
              namespace: 'default'
              manifests: |
                $(Pipeline.Workspace)/manifests/deployment.yml
                $(Pipeline.Workspace)/manifests/service.yml
              containers: '$(containerRegistry)/$(imageRepository):$(tag)'
              imagePullSecrets: '$(imagePullSecret)'
```

That's where thing get interesting, as you not only get access to a fully traceable set of information about your deployments, but also to key information about the health of the cluster and the related YAML configuration files in actual use.

![](/images/posts/2021-02-07_13-31-44.png)

![](/images/posts/2021-02-07_13-36-30.png)

![](/images/posts/2021-02-07_13-41-24.png)

You can even peek into the actual cluster application logs!

![](/images/posts/2021-02-07_13-42-08.png)

It's transparent, yet it provides so much value directly within the Pipelines hub. Now, this might be me being over-enthusiastic, but a good facilitator is always welcome and in this case Azure Pipelines provides a user experience I still consider second to none! 