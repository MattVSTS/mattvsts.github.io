---
layout: post
title: CI on GitHub Actions, CD on Azure Pipelines
tags: [github, pipelines, artifacts]
---
If you want to start approaching GitHub Actions, you can easily do that targeting Continuous Integration. 


However, when it comes to the deployment side of the story, it can be more difficult. Requirements can be different for everyone, and Pipelines as of today has an established set of patterns and features people already use.

Also, when it comes to GitHub Packages, there is one key missing item compared to Azure Artifacts: Universal Packages. They are a very effective way of moving stuff around, and as of today GitHub Packages does not support them.

So you want to use GitHub and GitHub Actions for all things development. It's not a problem, you will setup a workflow and build your stuff. But for deployments you want to use Azure Pipelines because you are already very familiar with it, you use Service Endpoints extensively, or whatever other reason. 

Nobody is stopping us from integrating Actions and Pipelines, with Azure Artifacts in between. It is relatively simple, and it provides good flexibility.

Let's take a step back: what do you do with _any_ project in your organisation? You run a CI engine that produces an artifact. That artifact can be deployed on multiple target environments, often also outside of your own project if you are working on a platform team or you are doing inner source.

Taking for granted you are already building your artifacts as part of the build process, all you need to add a couple of Actions to your workflow:

```
    - name: Publish package
      uses: Azure/cli@v1.0.0
      env: 
        AZURE_DEVOPS_EXT_PAT: ${{ secrets.AZURE_DEVOPS_PAT }}
      with:
        azcliversion: 2.0.72
        inlineScript: |
          az extension add --name azure-devops
          echo ${{ secrets.AZURE_DEVOPS_PAT }} | az devops login --organization https://dev.azure.com/<orgname>
          az artifacts universal publish --organization https://dev.azure.com/<orgname>/ --project="Your Project" --scope project --feed <your feed name> --name <artifact name> --version 0.0.${{ github.run_number	}} --description "Description" --path <path of your artifact>
      
    - name: Azure Pipelines Action
      uses: Azure/pipelines@v1
      with:
        # FQDN to the Azure DevOps organization with project name
        azure-devops-project-url: 'https://dev.azure.com/<orgname>/Your%20Project'
        # Name of the Azure Pipeline to be triggered
        azure-pipeline-name: '<your pipeline name>'
        # PAT
        azure-devops-token: ${{ secrets.AZURE_DEVOPS_PAT }}
```

Again, in Actions you have no Service Endpoint infrastructure so you have to deal with the cli directly. The first action uses the Azure CLI with a PAT added to the Secrets section of your project - you then add the azure-devops extension, authenticate and then publish a Universal Package to Azure Artifacts.

Authentication is quite tricky here - despite all my efforts, I still had to echo the PAT before logging in. The Azure DevOps CLI does not support either Service Principals or PAT as a parameter, so I had to go that way. It does not leak in the Actions log, but the environment variable alone **was not enough** to successfully authenticate. 

The reason why I chose a Universal Package is because it allows for easy and transparent flow of packages regardless of the content. If you are using MSDeploy for example, it is the way to go. Don't pay too much attention to the use of the GitHub Actions Run Number, I just needed a quick incremental number to use for versioning.

This process will publish the artifact(s) on the feed specified. Using a feed enables easy sharing of artifacts not only between GitHub and Azure DevOps, but also within projects contained inside the Azure DevOps organisation if the feed is configured as org-wide.

The second Action invokes an Azure Pipeline, and it doesn't require too much effort: FQDN, pipeline name and PAT will be enough to get you going. Of course that Pipeline should consume the feed we just published to!

This is all it takes to integrate the two platforms - it is fairly straightforward once you iron out the differences. A question I got while discussing this is:

> Why don't you use GitHub Releases or GitHub Packages as artifacts repository?

Obviously I chose Azure Artifacts because I wanted to integrate Azure DevOps and GitHub within my context :-) but there are other reasons: I did not use GitHub Releases because I wanted the artifacts to be independent of the repository at GitHub level, effectively making the code and CI side of the story pluggable. I also didn't want to tie down the deployment pipelines with an artifact source. 

The reason why I didn't use GitHub Packages is simple: there is no support for a generic (Universal) package which can contain a MSDeploy package. MSDeploy is used fairly heavily, especially when deploying on Azure - I might be changing the underlying DevOps platform, but I am not going to revamp a situation where things are already established and well-oiled.