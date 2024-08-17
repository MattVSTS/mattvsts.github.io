---
layout: post
title: Abstraction is acceleration
tags: [architecture]
---
Something I see far too often is a simple yet foundational mistake: chasing innovation at all costs, for the sake of it, rather than thinking about the key fundamental issues we are yet to solve as an industry.

Shipping quality software is the most important thing, no matter how cool or boring the underlying technology is. This is by far the most important metric we have, and if you really want to get going on that you need to embrace a simple approach: abstraction is acceleration.

### What do you mean?
The moment you start abstracting, you are moving complexity away from the narrow path of delivery and onto a different bucket. It does not mean removing it, but rather assessing it as a known quantity and treating it as an acknowledged factor.

Abstracting means removing yourself from the shackles of repetition for all the must-haves, so you can focus on doing what really matters for your project - it can be about infrastructure, application stacks, configuration, anything. It creates a runway which gives you the focus you need on solving the problem at hand, rather than being diverted onto different things which should be solved by now.

### An example
A typical example of this is [`azd`](https://learn.microsoft.com/en-us/azure/developer/azure-developer-cli/install-azd?tabs=winget-windows%2Cbrew-mac%2Cscript-linux&pivots=os-windows). Azure Developer CLI is a pretty advanced form of abstraction, which enormously simplifies developers' life by aggregating well-known infrastructure, application code and configuration in a single package.

![alt text](/images/posts/20240817.1.png)

This package is consumed as-is, giving you certainty about the steps performed during deployment: bringing up the infrastructure (via Bicep or Terraform, pretty standard stuff!), deploying the application correctly, etc.

Also very importantly, it is independent from any form of orchestrator - all you have to do is to invoke `azd up` even if you do not populate the `.azdo` and `.github` folders. It creates a repeatable experience independent of the execution environment, which is a must nowadays for developers. 

If instead you want to build your pipelines around it, these two folders are the place where you store them so that they are integrated in the package.

### You only accelerate if you are transparent
Be careful of an easy fallacy: you do not accelerate anything if the whole thing is not transparent. Abstracting doesn't mean "yeah submit a manifest and trust me on execution" in an API call, it means encapsulating a number of steps together in a pre-configured yet reviewable process.

The reason why `azd` is a good example is because you have everything aggregated, yet it's nothing new or opaque: your Infrastructure as Code definitions, your application code, your CI/CD pipelines - they are just kept together by a simple conventio, however they are independent of each other.