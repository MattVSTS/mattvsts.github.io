---
layout: post
title: Redeployments should not be difficult
tags: [devops]
---
It's a topic that comes up fairly frequently with many of my clients - why are redeployments unexpectedly difficult?

Now that DevOps is as pervasive as it's ever been, people are (rightly so if you ask me) trying to do as many things `as Code`. It's a testament to how the industry is going in the right direction, however the reality many developers face is that `initial deployments as Code` are very easy, redeployments... less so.

More often than not, it's simple stuff. For example, if you are relying on something as simple as a synchronous interaction with a system, all you might need is a form of [retry logic](https://mattvsts.github.io/2021/08/04/on-repeatable-automations/) to solve the problem.

Some other times, it's more complex - your system might need a full-fledged set of activities which will inhevitably result in some downtime. The first thing to do here is to leverage features like [Deployment Jobs](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/deployment-jobs?view=azure-devops) in Azure DevOps or [Environments](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment) in GitHub Actions.  

Both are almost mandatory tools nowadays, because they expose functionalities you would otherwise need to build manually for quality of life. For example, in Azure DevOps you can inject tasks via decorators or create a canary deployment strategy with a single line of code. In GitHub Actions you have excellent concurrency management as well as `cancel-in-progress`, a brilliant feature which will automatically cancel anything in progress if you need higher priority against other workflows.

It's then down to your technology stack and your architecture. These are unfortunately often overlooked, or straight-up impossible to achieve in brownfield enviroments, however there is a general tendency of overlooking papercuts and tolerating certain compromises. 

For example, if you ask me... Zero-touch deployments are a must. Idempotency is a key factor. These should never be compromised upon. If you cannot achieve idempotency you should automatically fall back to Blue-Green deployments as a pattern, as you risk ending up with unusable enviroments. Blue-Green in this instance prevents you from losing a functioning environment, and with zero-touch deployments you can still rebuild an environment.

It takes a lot of effort to get to a real zero-touch, robust and resilient enterprise systems. However it does not take a lot to start or improve an existing situation.

