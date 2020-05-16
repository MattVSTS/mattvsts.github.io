---
layout: post
title: Azure DevOps as the FinOps enabler
tags: [platform]
---
I recently spent a lot of time working on this topic, which in a nutshell can be summarised as:

> Can I make Azure DevOps my FinOps enabler instead of re-inventing the wheel?

Let's take a step back. FinOps? Yes, FinOps.

## FinOps is a reality of the world we live in
If you are using the Public Cloud, you are effectively using a utility. Hence, you are billed by a meter reading, and the more you use the more you pay.

FinOps is an engineering specialisation that bridges the gap between the world of financial management (there is still a procurement function in every organisation, and guess where the purchase order for an Azure subscription is screened and approved or rejected?) and the technology side.

The name is carefully identified as FinOps because of that - it actually stands for _Cloud Financial Operations_, but it is not trying to rip-off the success of DevOps. 

It is a deliberate choice based on the fact that one of the DevOps pillars is about removing silos and communication barriers. FinOps does applies the same treatment to Procurement (the people actually paying for the cloud resources) and Engineering Operations (the people using these cloud resources).

## Why Azure DevOps?
Think about it for a moment. With Azure DevOps (and Azure Pipelines in particular) you can have total control over the automations that provision and deploy the cloud resources you are going to use.

Pipelines can be scheduled, and Service Connections allow you to connect to anything in Azure, from a Management Group down to an individual Resource Group, and you can always execute either PowerShell scripts or ARM templates against Azure to achieve the desired state.

![](/images/posts/2020-05-16_09-43-06.png)

It doesn't take too long to understand that these are all the tools you need to empower your development teams towards a smart cloud usage.  

## It works regardless
Remember: you are on a meter, you pay for what you use. Do you really need that development environment running 24x7? Perhaps not, and you might make your application more resilient to restarts in the process of implementing that.

Each team can and should integrate this core FinOps principle in their habits and procedures so that it becomes part of the fabric of your organisation.

You might have circumstances where a team doesn't want to collaborate, or maybe there are other constraints limiting their involvement. This is not a problem with Azure DevOps, as long as you have a Service Principal that can connect to the target Azure resources.

If you need to go down the centralised management route, take advantage of YAML pipelines. Create a dedicated Git repository containing all the infrastructure pipelines you need, so you get a clear auditing trail.

Also leverage Environments as much as you can in the process - they cost you nothing to implement them and you also get a clear separation for visibility purposes.

