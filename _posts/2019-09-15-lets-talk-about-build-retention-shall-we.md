---
layout: post
title: Let's talk about Build retention, shall we?
tags: [platform, pipelines]
---
Build Retention Policies have always been a contentious thing to talk about: at some point, you need to let go of your old builds.
This post is not about **after how long**, but to talk about a couple of things to consider which might not be immediate. 

[Retention policies](https://docs.microsoft.com/en-us/azure/devops/pipelines/policies/retention?view=azure-devops) are applied at project level:

![](/images/posts/2019-09-15-18-58-59.png)

You have three settings to think about: how long you want to keep your _artifacts and attachments_, your _runs_ and your _pull request runs_. A _run_ is the actual build run, and it overrides both the other settings:

![](/images/posts/2019-09-15-19-02-31.png)

You can keep a run for up to two years, but artifacts and attachments will be gone after two months and PR runs after one. This is the topmost setting you can have, and it makes sense at the end of the day: you don't want to clog your organisation with stuff that is effectively not useful in the longer run. If you want to store your artifacts for more than two months you should publish your artifacts in a proper way (Azure Packages springs to mind...) rather than relying on the build run.

Then the elephant in the room: _how should I version my build runs?_

Long story short, you should have a way of easily identify your builds. It can be [GitVersion](https://gitversion.readthedocs.io/en/latest/), it can be [Semantic Versioning](https://semver.org/), it can be something else...but don't leave them to the standard naming convention as it won't make your life any easier.

Do not rely on the $(Rev:r) counter - you need to be in control of your builds, and be able to come back to a certain build if needed. Using $(Rev:r) isn't a feasible solution in the long run and also, bugs might [hit](https://developercommunity.visualstudio.com/content/problem/576040/successful-builds-no-longer-retained-so-buildnumbe.html). I was affected by this one, and there was no way back. 