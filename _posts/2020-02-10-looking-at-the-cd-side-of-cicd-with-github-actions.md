---
layout: post
title: Looking at the CD side of CI/CD with GitHub Actions - also how to deploy ARM templates with it!
tags: [actions, pipelines]
---
It's been a while I wanted to spend proper time with GitHub Actions and compare it with Azure Pipelines. Today thanks to the storm this weekend I had some time to do so :-) It's a long and wordy post, be advised. And no, no TL;DR!

GitHub Actions is built on the same foundation of Azure Pipelines, so the Continuous Integration side is very much what I am expecting from it: a series of tasks (Actions) running on an agent (Runner). The definition is contained in a yaml file (by default within a _.github/workflows_ folder) and is stored in your Git repository.

![](/images/posts/2020-02-09_14-45-17.png)

Nothing out of the ordinary up to this point: you will be dealing with a slightly different syntax, but it pretty much to what Azure Pipeline does.

Now onto the Deployment side of the story, that's where things get interesting. GitHub Actions as of today has got no deep integration with any cloud provider, or any authorisation automation for external resources. 

The premise is completely different from Azure Pipelines - you can (and should) use standard tools so that your local workflow can be automated. Hence, all the work we usually do around Azure CLI, PowerShell, Bash, etc. can be ported to Actions with minimal changes.

There are several actions already available on the [marketplace](https://github.com/marketplace?type=actions), so stuff like deployments or integrating existing automations won't be an issue. Take [this](https://github.com/marketplace/actions/deploy-vm-from-vsphere-content-library) as a quite edge example: if you are running vSphere in your datacentre (so nothing to do with any cloud) you can deploy a VM from the Content Library with just one Action as part of your deployment.

As a consequence of not having an equivalent to the Service Endpoint in Azure DevOps, you need to handle your secrets manually. This will entail, in the case of Azure, creating a Service Principal via the CLI and then building your own JSON structure with the four parameters you'll need:

```
{
    "clientId": "<guid>",
    "clientSecret": "<another_guid>",
    "tenantId": "<different_guid>",
    "subscriptionId": "<separate_guid>"
}
```
Once you have this you can paste it into the Secrets section of your repository and then you will be able to consume it as a _Secret_:

![](/images/posts/2020-02-10_19-43-21.png)

![](/images/posts/2020-02-10_19-44-22.png)

Logging in with Azure will be the first thing to do on a deployment. After that (and assuming you have your ARM template available in the repositoru), given you do not have facilities for ARM deployments, you'll need to use the CLI:

![](/images/posts/2020-02-10_19-47-08.png)

Now, as you could guess there is no 'stage' or 'environment' equivalence. The way you can manage target environments by mapping environment variables to secrets, and consuming them within your yml file. 

There is also no daisy-chaining: an Action workflow cannot invoke another workflow without API workarounds or Webhooks. However you can call multiple jobs with _job dependency_:

![](/images/posts/2020-02-10_19-59-02.png)

Summarising, GitHub Actions is to Pipelines what the _shift left_ movement is to a developer: it adds transparency, and it is very simple to deal with. YAML (despite the different syntax to Pipelines) is still YAML, so nothing completely new out there, as well as the Actions marketplace.

Cherry on top over here - you can [invoke Azure Pipelines](https://github.com/marketplace/actions/azure-pipelines-action) from a GitHub Actions workflow so you can move back and forth between both platforms should you need it, getting the best of both worlds!

