---
layout: post
title: CI/CD YAML Pipelines finally GA!
tags: [pipelines]
---
YAML pipelines for CI/CD are finally [GA](https://devblogs.microsoft.com/devops/announcing-general-availability-of-azure-pipelines-yaml-cd/). Hooray!

There are a few changes which have been introduced fairly recently: resources, as well as a number of approvals and checks.

## Resources
Resources are the built-in mechanism for consuming resources as part of a pipeline. 

```
resources:
  pipelines: [ pipeline ]  
  builds: [ build ]
  repositories: [ repository ]
  containers: [ container ]
  packages: [ package ]
```

This is the syntax to use when it comes to multi-repository builds, composition as part of releases, etc. 

In real-world situations you can have a situation where you have to deal with these (and more), so you are not tied to a single repository. Also, they enable a very interesting scenario: a reusable repository containing pipeline templates, which you can re-use across your organisation. A very cool example of inner source.

## Approvals and checks
This has been a long-standing request before GA: you need to have approvals, you need to control how releases progress from environment to environment.

![](/images/posts/2020-04-29_16-05-15.png)

Now, it's not just about _approvals_ here. You can also invoke an Azure Function, a REST API or query Azure Monitor like we did in the old Release Gates. My [AvailabilityFunction](https://github.com/MattVSTS/AvailabilityFunction) was designed for that!

At the same time, the bottom check is extremely interesting - requesting a _Required template_ you can make sure certain stages adhere to a certain convention across the organisation. It's pretty much the equivalent to a blueprint:

![](/images/posts/2020-04-29_16-09-26.png)

_Evaluate artifact_ is another one worth a mention. [Artifact policy checks](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/artifact-policy?view=azure-devops) have been around for a while, and they currently apply to container pipelines. They act as a gatekeeper with a set of policies that cover many things, from what ports are exposed to which images are consumed - providing again not only a level of standardisation but also an automated validation which can prevent security or quality issues.

![](/images/posts/2020-04-29_16-18-57.png)

I am a massive fan of Pipelines as Code, especially in the Azure DevOps implementation. You have all the power of YAML and Pipelines as Code (including versioning and reproducibility, which are the two most important ones IMHO!) together with an easy UX when building them thanks to the Task Assistant.  

Now they are GA for the release side as well, so there is no excuse for **not** using them :-)