---
layout: post
title: Challenges of creating an internal sharing model with Azure DevOps
tags: [platform]
---
Azure DevOps is a brilliant platform with a flexibility second to none, so it comes fairly natural to try and push its boundaries more and more when you start experimenting with its feature.

A very interesting problem came up in the last couple of weeks:

> I am trying to create an internal sharing model (also known as _Inner Source_) within our Azure DevOps organisation, but I am stuck on the visibility front. How can I make sure that users of different, segregated projects all get access to the same, shared project?

It is an interesting situation indeed. And guess what, it all boils down to a couple of points.

Looking at the individual services, everything looks so easy - the easiest to tackle is Azure Pipelines - cross-Team Project consumption is trivial to setup, so that is definitely off the problems' list.

Azure Repos itself, not an issue - it is a Git repository after all, and features like [Forks](https://docs.microsoft.com/en-us/azure/devops/repos/git/forks?view=azure-devops&tabs=visual-studio) make this a very valuable component. Each user will be able to fork from/to the shared set of repositories in a completely transparent way.

Azure Test Plans...nothing to mention, really. 

Azure Boards has got an interesting challenge, which highlights the most complex problem you will face in this exercise: you cannot re-use existing Project Groups nested into different Groups.
This throws a massive spanner in the works, as if you are creating an Inner Source model you don't want to handle permissions at a granular level, but you want as much inheritance as possible when it comes to accounts. It doesn't make sense to authorise a user directly, expecially if you have a large organisation - the management overhead becomes quickly too much to handle.

You also cannot take the shortcut of leveraging the **Project Collection Valid Users** group - that is locked down, and unless you start fiddling with _tfssecurity.exe_. You can do that, but what stops me (and should stop you) is that you are forcing a group you are not supposed to use. It can work, it works, but from a supportability point of view it can become a risk - and if you have a very large organisation I am not sure it is the best way forward.

So, what are we left with? Aside from adding users directly (again, no!), if the organisation is setup in a smart way you will likely have your AAD synchronised with an on-premise Active Directory forest. That means your AD groups can be leveraged in Azure DevOps, and the users contained in there will inherit the access permissions.

![Permissions](/images/posts/2019-08-10-12-27-05.png)

With that in mind, you can build your Inner Source security model around AD groups (which should already control user access, as Active Directory - or any other directory service for this matter - should be the main way of handling access) mapped to Azure DevOps prather than directly into the Team Project, and then assign the group(s) to the Inner Source project. 

![add](/images/posts/2019-08-10-12-31-02.png)

Of course it is not something you will do for every organisation. If you have small organisations you might accept managing the users. If you are using a single Team Project, you don't have this problem at all. As usual, the real world is the most varied of the demo scenarios, there is no one-size-fits-all solution.