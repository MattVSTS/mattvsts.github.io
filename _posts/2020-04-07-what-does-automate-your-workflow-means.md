---
layout: post
title: What does "automate your workflow" means?
tags: [github, actions]
---
GitHub's marketing headline is [very clear](https://github.com/features/actions) IMHO:

![](/images/posts/2020-04-07_14-23-11.png)

But marketing aside, what does it **actually** mean? 

GitHub Actions is not _just_ a CI/CD engine, its integration with the platform goes much deeper. The more I spend time with it, the more I find out these perhaps simple but (to me!) valuable bits. 

It's true that we often bend Azure Pipelines [to do things](https://mattvsts.github.io/2019/06/30/remember-the-power-of-an-agent/) which are not really within the defined scope of work, but that's a side-effect of Azure Pipelines being extremely flexible. Pipelines is a CI/CD engine that can be a general purpose orchestrator, Actions is the other way around.

Let's say, you might be here because of a tweet like this:

![](/images/posts/2020-04-07_14-32-46.png)

That tweet was not manual. That tweet is the output of my custom workflow (thanks to [Ed](https://www.edwardthomson.com/blog/github_actions_30_integrating_other_apis_in_an_action.html) for his Action!):

![](/images/posts/2020-04-07_18-50-37.png)

This workflow runs on every push to master, unless the commit message includes **NO CI**. If the workflow is running it will pick up the comment from the commit (which by convention it is always going to be the title of the post) and tweets it in a pre-built body.

"Automate your workflow" means this. Not just CI/CD, but an underlying orchestrator spanning across the platform, where the main artifact is code.