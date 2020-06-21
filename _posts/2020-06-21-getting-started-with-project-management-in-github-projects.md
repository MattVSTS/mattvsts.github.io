---
layout: post
title: Getting started with project management in GitHub Projects
tags: [github, issues]
---
If you want to approach GitHub Issues for your projects, sooner or later you are going to need a form of project management. It can be Azure DevOps (and I am very keen [on it](https://mattvsts.github.io/2020/04/22/synchronising-github-issues-and-azure-devops-work-items/)), but what if you want to retain everything within GitHub? The answer is GitHub Projects.

GitHub Projects is definitely designed around a board and a Lean process - all of the default Template options point at that direction:

![](/images/posts/2020-06-21_17-29-08.png)

**Automated Kanban** will get you started with a good amount of helpers to get it off the ground. You can also link repositories to a board, which is the best way of populating a board:

![](/images/posts/2020-06-21_17-31-47.png)

For our example, let's pretend I am creating a board that unifies the GitHub Issues the teams are working on and provides a unified pane of glass for all the current activities. If you are starting from scratch, then you are done - you get a board, and you can start adding stuff to it:

![](/images/posts/2020-06-21_17-42-04.png)

What you see there as cards are not necessarily Issues coming from repos - you can also have independent cards, and everything is markdown-based anyway so they are easy to edit.

In the real world it is quite unlikely to start in a nice, greenfield situation. More often than not you will need to setup a Board for an existing repository, which might already have a number of issues making up a backlog.  

In that case, the first thing to do would be to add the issues you want to this board. I linked two repositories with existing data, hence I need to add these:

![](/images/posts/2020-06-21_17-46-31.png)

![](/images/posts/2020-06-21_17-48-51.png)

You can do it manually once or twice, but after a while it becomes an overhead...  

Needless to say, we have automations. If you set the **Projects** property for an issue, it will be automatically be linked to the Project:

![](/images/posts/2020-06-21_18-00-46.png)

![](/images/posts/2020-06-21_18-01-20.png)

![](/images/posts/2020-06-21_18-02-14.png)

Also, any issue set to a Closed state will automatically go to to the Closed column.  

All nice and good, but it's not enough to have a simple setup out of the box. A key missing bit, for example, is that you might want to move an issue when it's assigned to someone into the **In progress** column, and the out of the box automation doesn't do that. 

That is where GitHub Actions enters the picture - thanks to [one](https://github.com/marketplace/actions/create-or-update-project-card) of the many actions in the marketplace you can create a workflow like this, and every time an issue gets someone assigned it will be automatically moved to that column:

![](/images/posts/2020-06-21_18-30-40.png)

By implementing this workflow to any linked repository you will get a nice and smooth management experience for a Lean backlog. There is obviously much more to it, but it is a starting point to real project management in GitHub.