---
layout: post
title: Beware of implicit triggers in Azure Pipelines!
tags: [pipelines]
---
I was talking with [Mohamed](https://mohamedradwan.com/) about this earlier today - it's something that can make you think you are off the track while in reality there is a much simpler explanation :-) 

Let's say you have this pipeline - the traditional:
```
pool:
  vmImage: 'ubuntu-latest'

steps:
- script: echo Hello, world!
  displayName: 'Run a one-line script'
```
This is a CI build - you have no trigger, but as per documentation you have an implicit trigger on all branches (as per [documentation](https://docs.microsoft.com/en-us/azure/devops/pipelines/repos/azure-repos-git?view=azure-devops&tabs=yaml#ci-triggers)).

![](/images/posts/2020-11-25_18-54-20.png)

The main thing to be aware of is that this type of trigger will operate on all branches, and on **all events**. All events include **branch creation** as well, so don't be surprised if you see a slew of pipelines running when you create a branch - chances are you are using an implicit trigger and they are running as expected!