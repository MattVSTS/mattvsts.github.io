---
layout: post
title: "No message found for this issue" in Azure DevOps
tags: [pipelines]
---
I am writing this post because I've been asked four times within two weeks, so it acts as a public service announcement :-)

![](/images/posts/2020-11-10_17-02-54.png)

The stage is still successful. Looking deeper into the execution by setting ```System.Debug``` to ```true```, you can see in the logs that it might have got to do with the Service Principal in the ARM deployment task:

![](/images/posts/2020-11-10_17-07-15.png)

In reality, it doesn't - there was definitely some change to the out-of-the-box task, as this is not the expected behaviour.  

[This](https://github.com/microsoft/azure-pipelines-tasks/issues/13797) GitHub issue explains what the problem is, and hopefully it will be sorted soon!