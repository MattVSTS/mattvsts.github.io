---
layout: post
title: DevOps in a Landing Zone, how to run commands across it with Azure Resource Graph
tags: [pipelines]
---
I am currently working with a client that's got a very well made [Landing Zone](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/)  (we are talking tens of subscriptions with nested Management Groups), and my team is building Azure Pipelines running automations that need to span across the whole Landing Zone.  

If you ever find yourself in this situation, remember that Azure DevOps is very well equipped for this - you can register Service Connections that span across Management Groups, including the root one:

![](/images/posts/2020-09-05_12-36-38.png)

That said, even if you build something that can potentially be generalised to the whole Landing Zone, you will quickly realise that you have a problem: _scoping_.

_Scoping_ for an Azure command means that whenever you run anything against it you will always be scoped to a subscription. [Set-AzContext](https://docs.microsoft.com/en-us/powershell/module/az.accounts/set-azcontext?view=azps-4.6.1) is a very clear example of this, and obviously while you can work around it by looping any command across all the contexts your account or Service Principal has got access to, in a Landing Zone this quickly becomes an unnecessary overhead.

So how to solve this problem? The answer is [Azure Resource Graph](https://azure.microsoft.com/en-us/features/resource-graph/).

An Azure Resource Graph query can span across the whole Landing Zone. Let's say you want to deploy an update to every App Service running in a certain location. If you have tens of subscriptions where you need to perform this, it can be a big task. With Resource Graph, you can retrieve the information required like this:

![](/images/posts/2020-09-05_12-51-15.png)

and then run the query with `az graph query -q "<your inline query>"`. The list of Resource IDs can then be used as an input for the many Azure commands you might want to use, and taking away the requirement of scoping to a subscription or a Resource Group.