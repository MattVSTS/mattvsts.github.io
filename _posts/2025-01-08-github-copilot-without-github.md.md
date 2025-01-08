---
layout: post
title: Can I get GitHub Copilot without using GitHub?
tags: [github]
---
I entertain this question at least once a week so let's put a reference answer out once and for all 😀 

> I want to use GitHub Copilot but I am using a different development platform. Can I use it anyway or do I need to migrate to GitHub?

### Short Answer
Yes, you absolutely can. GitHub Copilot primarily lives in the IDE so your code can live anywhere and you can use it.

### Long(er) Answer
What organisations are mostly interested in are the Copilot Business capabilities, and GitHub Copilot is a developer tool, so it can be used on *any code, anywhere*. Even when the code is not in a Git repository at all. 

It is also a SaaS product, so all it requires is somewhere for it to be billed to, which however needs to remain under organisational control for governance and compliance. It is called [**GitHub Copilot Standalone**](https://docs.github.com/en/enterprise-cloud@latest/admin/copilot-business-only/about-enterprise-accounts-for-copilot-business), and it is essentially a GitHub Enterprise organisation with no enabled features except for Copilot Business.

In order to get it, you need to contact the lovely sales folks at GitHub, and they will setup this special organisation for you.   
Once done, you need to then connect an Azure Subscription so they can bill the metered usage of the product and you can start setting up teams for licence distribution to your developers. You can do this under the **Billing** settings in your Enterprise.

![](/images/posts/2025-01-08-20-41-00.png)

That's all! I hope this helps. Thanks for asking 🙂