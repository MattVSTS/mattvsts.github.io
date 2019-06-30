---
layout: post
title: Remember the power of an Agent
tags: [pipelines, automation, thoughts]
---
This post stems from a discussion I had a few days ago: sometimes we just forget how powerful having an Agent on a target system can be.

The example in case is for a well known financial product, which usually runs in a network isolated from the internet and with very limited access from operators. You want a degree of controlled access without resorting to complex solutions (AAD Conditional Access, etc.) or products because of other limitations. You cannot leverage Azure Automation as well with its Hybrid Runbook Worker because of the non-existent internet access. What's left?

Enter Azure DevOps Server in this scenario. Once you install an Azure Pipelines agent on the target machines you have an easy way of leveraging all sorts of automations (including custom scripts if you **really** need them!) in a tightly controlled fashion. Once the permissions are clearly locked down (and approvals are in place at every required stage) you can use the linked Git repositories or TFVC paths to drop whatever you need on the targets, automate routine tasks, perform scheduled operations.

You get the authentication layer for free, courtesy of Active Directory. You get an integrated artifact funnel thanks to either Repos or Artifacts. You get several out-of-the-box ways of performing automated tasks and you get an orchestrator to coordinate these tasks.

If you think about it from a non-technical point of view, how much effort would it take to build up something like that from scratch or integrate a number of different technologies to do all of the above? A lot, I reckon. Which is why one should never forget _the power of an Agent_ :-)