---
layout: post
title: Retry logic in Azure DevOps tasks
tags: [DevOps]
---
Large yet quiet update a couple of months ago in Azure DevOps! One of the most requested features finally hit availability - [retry logic in all server tasks](https://learn.microsoft.com/en-us/azure/devops/release-notes/2024/sprint-240-update#retries-for-server-tasks).

Every task that runs in a job with a stateful environment (e.g.: anything except agentless tasks) was already supported, however this is now extended to tasks invoking an external service. They will now have an available property named `retryCountOnTaskFailure`, which can ve used to set a number of retries once execution fails. 

Imagine... you are performing an operation targeting a remote URL/system/etc, and you will be able to retry. It is extremely useful, especially when publishing new bits on Azure resources. It's not by chance that the Microsoft documentation shows `AzureFunction` as a sample task supporting this!

Now, there is an important consideration to make: your task is not idempotent. Do not expect rollbacks or structured retries, only the task (and the external call) is retried in its entirety, not the job or stage. You still need to account for failures etc, however this simplifies your pipeline design if you are using tasks extensively.
