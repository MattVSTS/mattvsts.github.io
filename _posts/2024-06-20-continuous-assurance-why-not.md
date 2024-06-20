---
layout: post
title: Continuous assurance, why are you not doing it?
tags: [architecture]
---
Baffling conversation today, and a bit of a blast from the past. Mega-massive client has issues with their immutable environments - technical and regulatory. The regulatory stuff is relatively easily to fix once the technology is in place, and the summary of the conversation was: _what can you do to remediate, quickly?_

The answer is obviously _Continuous Assurance_ but... we will get there. You need a starting point.

Let's ignore development environments, they should be ephemeral and deployable on the fly, and they weren't. However in this case the issue is deeper: the client is unable to reliably replicate an environment from scratch, or at will, to create a new copy of a production environment because there is drift between the production, pre-production environments and the scripts used to deploy and configure. 

It's a serious matter, as you cannot guarantee testing integrity, you cannot ensure that the pre-production environment is actually configured as expected, an audit will not succeed, etc. What could you do here?

Ideally there should be a foundational set of automations doing this on the Landing Zone (look at [AzTS](https://aka.ms/devopskit/AzTS)), but if you are starting with dev-driven bottom-up approach, you can do this: besides the expected review of procedures, scripts, etc. the idea is to embed Continuous Assurance as the leftmost step in the deployment procedure so that _any_ release will validate the environment state.

And this is where things are simple to start with... if you deployed your environment with a Terraform module, what do you have? 

> a state file!

Exactly. And if you are not using Terraform you can achieve something similar by refreshing (not rebuilding, they are immutable!) the environment every release, and ensuring a re-application of your configuration as the first step.
It sounds incredibly simple, yet you would be surprised by how many times this detail is overlooked. Gotta go back to basics and remember the technologies we are using on a daily basis.

If you do not have a state file (ARM, Bicep, etc.) then the refresh process for an immutable environment will always start with the infrastructure and configuration refresh. There will always be things to take into account: you might need to backup/re-image/restore/etc an environment, or build an allocation mechanism for finite resources such as API interfaces, but implementing this from the ground-up will give you the confidence you need in your immutable environments. 

### Azure DevOps

Azure DevOps also gives you some strong accelerators for this, and they have been around for a long time! **Environments Checks** for example:

![](/images/posts/20240620.1.png)

Alternatively, build a [deployment strategy](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/deployment-jobs?view=azure-devops) supporting this proces. A hint: `preDeploy` hooks are fundamental for this. 
Worst case scenario if you don't want to use them, Azure Pipelines allows you to create `stages` with a few extra lines of code. I am yet to hear a convincing enough answer to why you are not using them 😂

### GitHub Actions

GitHub Actions does not give you these facilities given it is a platform-level orchestrator, however it's not the end of the world - you can easily build a sequential orchestration leveraging the `needs` attribute for a job:

```
preprod_refresh:
...

preprod_deploy:
    **needs: preprod_refresh**
    ...
```

This is flexible enough to perform any form of operation required for an environment refresh. 

It's simple stuff, really, and obviously it's not the end of the topic, but rather the beginning. But following this will allow any team to put these in practice quickly in absence of a platform-wide Continuous Assurance facilitation. 