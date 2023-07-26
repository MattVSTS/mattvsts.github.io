---
layout: post
title: Improve your environments with Azure Deployment Stacks
tags: [azure, devops, pipelines]
---
Are you doing anything like this?

![](/images/posts/2023-07-26_21-06-30.png)

If so, you should try [Azure Deployment Stacks](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/deployment-stacks?tabs=azure-cli). The feature was released in Public Preview a few days ago, and it is definitely worth looking at it as soon as possible.

Azure Deployment Stacks simplifies the resource lifecycle in Azure, it essentially groups together multiple resources under the same _stack_, removing the overhead of dealing with dependent resources and also applying effective policies improving governance

The documentation is heavily oriented towards Bicep, however it definitely works with ARM templates as well. And it works really well.

![](/images/posts/2023-07-26_21-13-45.png)

These are very welcome - the **Update behavior**  property mimics the ARM Deployment Mode, however taking the Stack into consideration. The **Lock** property is amazing, potentially putting anything under the Stack in a protected mode, simplifying governance and control. The rest is an unaltered deployment, via an `az stack` command. Redeployments take into account dependencies and the **Lock** property.

It is so simple it is mindblowing. Also... this considerably extends the usefulness of the Environments in Azure DevOps:

![](/images/posts/2023-07-26_21-22-02.png)

While it was true that you could have done that without Azure Deployment Stacks, you now have a repeatable, out-of-the-box command to create a 1:1 map between the Environment on the platform and the target environment in Azure.  

Done at scale, this significantly simplifies the life of Platform Engineering teams.