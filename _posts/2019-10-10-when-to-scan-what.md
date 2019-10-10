---
layout: post
title: When to scan what?
tags: [DevSecOps]
---
Picking up from my [last](https://mattvsts.github.io/2019/09/30/integrate-fortify-in-azure-devops/) post, a question I regularly get after showing these tools is:

> Should I apply all of these (_tools and practices_) to CI builds and canary releases?

The answer is clearly not. If you start running code quality checks, SASTs, DASTs, OSS compliance checks SVTs, etc. as part of a CI process these will become ridicously long and the value you *think* you are providing will go down the drain, lost in the sea of people screaming because your CI build now takes four hours up from the two minutes it used to.

Everything clearly has a place and a time.

There are no-brainers like OSS compliance scans for example - these should happen at every CI build. Doing it so early prevents the risk of adding an old/insecure/non-compliant library and causing issues down the line. Also, the overhead on the build process is minimal - we are talking a couple of minutes tops (from what I've seen).

Secrets detection is another one: you cannot afford to leak a password, access key or whatever other secret these days. It doesn't need more time spent on it.

Other things like code quality scans are more nuanced. My approach to these is to have different rulesets for different type of builds. A CI build to develop will have a different (looser) ruleset compared to a full master release. And it makes sense - if you want to merge a large development from develop to master for the first time chances are you focused on certain areas of the enhancement, which while being absolutely good and welcome it might cause issues within master. Different rulesets ensure you don't get bogged down in making it _green_ from the beginning, but you can spend time on these refinements closer to the moment you actually need to merge it. 

Infrastructure deserves its own chapter. Security Validation of IaC resources should always be a continuous process, because it is subject to continuous movement. Take IaaS for example. OS patches are enough movement to demand for a continuous process, without mentioning infrastructure vulnerabilities (even at network level). DevOps is simply the entrypoint for this practice - it is imperative to make it an organisational approach.

If you run Security Validation Tests regularly on your infrastructure, you will find out things that are usually brought up only _on demand_:

![](/images/posts/2019-10-10-17-50-08.png)

Doing so will not only save you a massive headache, but it will ensure you are going to proactively act on these areas rather than fixing things in a rush as a reactive effort. And this saves money in the longer run. Different security rules and analysis (again) at every step of the way - IaC analysis at build and release time, but then continuous assurance at structural level, as a separate process from the development workstream.

It is also connected to Security scans - both static and dynamic.

A SAST (Static Analysis Security Test) is expensive to run - it can take hours to complete a run. A DAST (Dynamic Analysis Security Test) alone might not be enough. Having a structured chain of checks and balances, with different tools, rules and layers along the way from the IDE down to the Production environment is going to make all the difference in the world when it comes to DevOps. 

SASTs should be performed in parallel to all the other testing activities. 
DASTs can be run as part of the performance and reliability testing. 

This mix ensures a good level of agility for delivery (you still need to deliver your value as per DevOps definition!) while balancing it with a strong, 360 degree approach that ensures no stone is - hopefully - left unturned during the journey.