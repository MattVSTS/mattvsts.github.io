---
layout: post
title: How YAML pipelines change the whole CI/CD story
tags: [pipelines, powershell]
---
At Build the Azure DevOps team [announced](https://devblogs.microsoft.com/devops/whats-new-with-azure-pipelines/) YAML pipelines for the deployment side of the story.
I am very excited, because I believe this changes the whole CI/CD proposition not just for Azure DevOps as a platform but in a broader sense. 

For years, I've been talking around at conferences and meetups about the fact that in a true DevOps world we only have to deal with packages (coming out of builds) and orchestrators (handling deployments). 
The whole concept of Build or Release Definition has been slowly merging, and now we are at a stage where we can see a truly unified orchestration story.

So, if in the past you were used to this:

![old](/images/posts/20190510.1.png)

now you need to get used to this:

![new](/images/posts/20190510.2.png)

The fact is - the division is going away. It was already close to non-existent before with the task-based model, but now it is completely gone.
To take advantage of this, all you need to do is structuring your yml pipeline as follows:

```
stages:
- stage: Build
  jobs:
  - job: Build
    pool:
      vmImage: 'Ubuntu-16.04'
    continueOnError: true
    steps:
        ...
- stage: Deploy
  jobs:
  - deployment: DeployWeb
    pool:
      vmImage: 'Ubuntu-16.04'
    environment: 'target'
    strategy:
      runOnce:
        deploy:
          steps:
            ...
```


The actual result of this pipeline is two stages: one dedicated to the build and the other one targeting a release:

![pipeline](/images/posts/20190510.3.png)

And the two jobs reported in the matching stage:

![jobs](/images/posts/20190510.4.png)

Of course the example is very simple and does not cover all the possible scenarios, but what this means is that you have an end-to-end pipeline definition from build to release - in different phases, defined by the type of activity you need to perform.

In a real-world situation, one of the things you can do is to split the Build and Release portion of the definition with templates, and pick it up from there. 
Then the orchestrator will instantiate whatever is needed by leveraging parameters, and you will not only get consistency but also the ability of re-using loads of work in a series of standard components.