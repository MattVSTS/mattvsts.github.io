---
layout: post
title: You've got no excuses in managing secrets with Azure DevOps and KeyVault!
tags: [pipelines]
---
As part of a solid engineering practices one of the first things I flag up during an assessment is how you handle secrets - their management is really one of these things where you cannot cut corners.

Azure KeyVault is awesome in this, as it is really set-and-forget. And using Azure Pipelines with KeyVault is really _stuff of the dreams_, as the integration between the two makes it really easy to consume.

Let's say you setup this secret named 'Key' in KeyVault:

![](/images/posts/2019-12-01_11-42-35.png)

Azure Pipelines and Azure KeyVault by default share a _convention over configuration_ approach, meaning that your secrets' key names in a KeyVault are automatically mapped to Pipelines variables with the same name. This makes it ridiculously easy to use!

All you need to do is to download the secrets you are interested in from your KeyVault as part of a build or a release, and use the relative variables. 

![](/images/posts/2019-12-01_11-51-46.png)

In the real world you would use it to deploy and configure your resources, but I didn't want to add additional overhead to the scenario - I just want to show you that **it works**. 

So I created a quick Pipeline that validates a secret with a control value to make sure it is correct - the **Key** variable is empty but encrypted to mark it a secret, the **ControlKey** variable is the value against which I want to check it:

![](/images/posts/2019-12-01_11-49-36.png)

Then this barebone PowerShell script is going to validate it on the fly:

![](/images/posts/2019-12-01_11-52-11.png)

Give it a go, I can guarantee it is going to work as expected :-) 

![](/images/posts/2019-12-01_11-55-30.png)

![](/images/posts/2019-12-01_11-56-45.png)