---
layout: post
title: Synchronising GitHub Issues and Azure DevOps Work Items
tags: [github, actions, boards]
---
Another integration between Azure DevOps and GitHub is in work planning and tracking, or project management if you like.

While from a technical perspective they will be achieved in a similar way, I believe we have a number of possible scenarios, with a couple of examples below:

>use Azure Boards for backlog management, as well as having an open source or inner source model where stuff is published to GitHub and issues from consumers are publicly logged from there.  

>be independent from the project and portfolio management side of the story, where the PMO rolls backlog data coming from GitHub Issues into Epics and Features hosted natively in Azure Boards.  

The solution is very straightforward - use Dan Hellem's [Action](https://github.com/danhellem/github-actions-issue-to-work-item) as it is, and mapping the Azure DevOps Work Item Type of choice to what makes the most sense in your circumstances. You could even use a different Area Path, if you want:

![](/images/posts/2020-04-22_21-44-53.png)

Let's say we are tackling the first scenario: in that case opening an issue in the GitHub world will create a Bug in Azure DevOps, so that external contributors will have an opportunity of opening something in your backlog, with various reminders of the connection to GitHub:

![](/images/posts/2020-04-22_21-49-00.png)

![](/images/posts/2020-04-22_21-51-53.png)

This also means that if someone, as part of a Pull Request, mentions that specific issue via the AB# syntax in a comment, commits will be automatically associated to the Azure DevOps Bug!

![](/images/posts/2020-04-22_22-02-54.png)

![](/images/posts/2020-04-22_22-01-23.png)

This enables a real contribution workflow at both ends, where the GitHub Issues are treated as first class citizens rather than an afterthought. 

The integration is deep both ways, as it requires the Azure Boards GitHub [application](https://github.com/marketplace/azure-boards) on the GitHub account or organisation, and it will automatically configure the GitHub Connection on the Azure DevOps side:

![](/images/posts/2020-04-23_17-33-07.png)

On top of that, take a look at the Action's [source code](https://github.com/danhellem/github-actions-issue-to-work-item) - extending that will open the Pandora's box when it comes to customising the Work Item created by the integration:

![](/images/posts/2020-04-23_17-36-55.png)

It is effectively a wrapper around the REST API, so you can tailor it down to your needs!