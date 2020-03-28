---
layout: post
title: A tour of GitHub Enterprise Cloud
tags: [github, organisations]
---
Continuing my exploration of GitHub from Azure DevOps, the next topic which caught my attention is the equivalence between Azure DevOps and GitHub at service level. I am particularly interested in GitHub Enterprise Cloud, which seems to be the closest match to what I am already familiar with!

## Organisations
In Azure DevOps Services the first thing you do is creating an _Organisation_ (it used to be _Account_ and it is a _Collection_ in the on-premise world). When you go to GitHub.com, what you create straight away is an individual account. How would that work with enterprise ownership?

The answer is the same, albeit slightly hidden: GitHub Organisations. It's not in-your-face that much - you can find the Organisations page under your Settings:

![](/images/posts/2020-03-28_07-54-53.png)

An organisation can totally be free - there is no cost attached to it if you use it for open-source development. If you need private repositories (and development) then you can create a Team plan or an Enterprise plan, with the relative cost.

Once you move towards Enteprise Cloud, getting into the Organisation side you will be faced with a set of familiar set of settings and menus, but there are a few differences comparing them with Azure DevOps'.

## Permissions and Security
All the ACL are handled under the _Member privileges_ menu, as well as various visibility settings.

For a user, there are four _base permissions_:

![](/images/posts/2020-03-28_08-22-44.png)

Unless a user is added to a specific Team or Repository, it will automatically inherit this base permission.

From the same page you can also expand the Forking capability to private repos, and control the Actions integration. This is interesting - you have three settings: _Disabled_ (I wonder who will ever disable Actions!), _local Actions_ and _local and third party Actions_. It is a nice way of enabling vetting for Actions should you need it - with the local Actions setting you are retricting usage to Actions where the code is contained within an Organisation's repository.

On the Security front you can require 2FA for all users contained in an Organisation (please do!), integrate SSO with your identity provider of choice, synchronise teams via AAD, add a SSH CA and implement IP whitelisting.

The last one is very interesting for the Enterprise world, and it is nice to see such transparency about it. It is worth knowing that once you enable IP whitelisting you lose the ability to consume the hosted GitHub Actions runners, and you need to host your own.

## Managing a project
Unlike Azure DevOps, you do not require a _Team Project_ in GitHub. The approach is different - everything revolves around code, so you can have loose repos where all the members of an Organisation can contribute. 

![](/images/posts/2020-03-28_08-02-54.png)

A _Project_ in GitHub is a set of features to enable a basic planning and tracking experience. One or more repos can be linked to a Project to facilitate suggestions and search. A Project can have a Project Template, but do not expect anything like in Azure DevOps - here things are very lightweight and prone to automation:

![](/images/posts/2020-03-28_08-08-45.png)

The **Basic Kanban** template is really the simplest one you can start from - all the automations from the other templates are implemented via GitHub Actions. 

You can immediately see that there is no choice between _Agile_, _Scrum_ or _CMMI_ in terms of templates, it is an experience completely decoupled from your process. Needless to say you can customise anything and everything.

## Teams
A Team is a way of grouping people and granting access to common resources together. You can assign Projects, other Teams and Repositories to a Team, so that all the tracking effort can be targeted by these groups.

![](/images/posts/2020-03-28_08-57-27.png)

The main aim of a Team is to facilitate discussions - they can be used to track decisions and conversations before formalising them in Project issues.

## Anything else?
That is it for Enterprise Cloud, the differences with Azure DevOps are pretty much summarised in the above list. 

What I **really** like is the lack of overhead. From an administrative perspective there is no need for a full-time role managing the organisation and things are really transparent. Teams can focus on creating value without spending too much time in administrative tasks, and there is a large focus on communication and information sharing within the platform.

We should also keep in mind that this approach doesn't require to go all-in with a massive change to the way teams work today. I am fairly sure only a relatively small percentage of teams will take advantage of **all** the features an Organisation can offer from the get-go, often because of longstanding habits and resistance to change. 

There is nothing wrong with it, and GitHub Enterprise Cloud is granular enough to offer a seamless experience regardless.



