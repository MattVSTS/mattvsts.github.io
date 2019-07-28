---
layout: post
title: What is the difference between Usage and Auditing in Azure DevOps?
tags: [governance]
---
The Azure DevOps team released a new [Auditing](https://docs.microsoft.com/en-us/azure/devops/organizations/settings/azure-devops-auditing?view=azure-devops) feature a couple of days ago, and then a question immediately sprung up: what is the difference between Auditing (the new feature) and Usage?

[Usage](https://docs.microsoft.com/en-us/azure/devops/integrate/concepts/rate-limits?view=azure-devops) is pretty much the old Operational Intelligence brought into a new UI and into the Cloud operating model: it is mostly about service health, and from there you can only get a live snapshot of what is going on. Data is flushed after 14 days and lists every call to the APIs. It can be used as an auditing tool, but it is not meant as such - you need to spend time filtering the log and extracting the information you need to get to a point where you can use that data for an audit. I [blogged](https://mattvsts.github.io/2014/03/02/how-to-perform-tfs-security-audit/) about [this]https://mattvsts.github.io/2014/07/07/tfs-audits-how-to-create-reports-on/) in the past.

Auditing is much more - it is a centralised place for **events** raised in Azure DevOps. An event is an access policy change, a Team Project creation or deletion, extension installation or update, etc. It provides a much different view over what happens to the service, and it is tailored down the needs of a real auditing process - it means no more fiddling with the log, no more overhead to extract the data you need.

The feature is currently under development, and it is going to receive interesting developments like [this one](https://dev.azure.com/mseng/AzureDevOpsRoadmap/_workitems/edit/1565788/).