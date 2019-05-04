---
layout: post
title: Solving the looping problem in Azure DevOps Pipelines
tags: [pipelines, powershell]
---
What should you do if you want to have a Pipelines job that loops based on dynamic inputs?
Working around this problem has always been a pet peeve of mine - luckily today we've got options! Three in total to be precise, with different degree of difficulty.

One of them is the simplest and has been around for ages: embed what you need to do in a script. Try to split the problem down to the lowest common denominator, and run the script.
I just did this in a situation where we needed to run a non-predictable number of SonarQube scans as part of a CI build. We had the whole codebase in the branch (because reasons...), and based off the standard folder structure used by the projects I put together a script that runs the SonarQube scanner based on the number of plugins changed in a certain commit. 

If you think about that, it's a very basic challenge. The _problem_ (I don't even want to call it as such, but still a challenge regardless) is that there is no built-in facility for such a concept, hence I had to improvise.

The second one is using a build definition to be used as a template. You can trigger a dynamic number of these from another build (with a REST API call) that acts as orchestrator. This is slightly harder, but it allows for the GUI-based definitions to be used as templates so you can re-use what you have and you know already.

The third (and better) way of doing so comes with the YAML pipelines: the [_each_](https://github.com/Microsoft/azure-pipelines-yaml/blob/master/design/each-expression.md) expression.

_Each_ in YAML is equivalent to a for loop. So you can create a template which will have a set of actions, and pass parameters across during your build. YAML is looser than a GUI-based build definition IMHO, so it allows for something like this:

template.yml:
![template](/images/posts/20190504.2.png)

azure-pipelines.yml:
![pipeline](/images/posts/20190504.1.png)

Doing this will create two inline script task totally on the fly:

![result](/images/posts/20190504.3.png)

It is a very elegant solution that solves the looping problem in the first place, but of course it has a steeper learning curve.

Regardless of what you choose, the flexibility of the platform is at such a level that anybody can find the solution which fits best given a problem. And it was good fun exploring them throughout :-)