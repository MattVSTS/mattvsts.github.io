---
layout: post
title: Where Supply Chain Management really matters
tags: [platform, security, dependencies]
---
If you use GitHub you are surely used to this:

![](/images/posts/2022-04-06_21-01-08.png)

Nowadays we are starting to take supply chain management for granted. Unfortunately it is a tendency as an industry - instead of focusing on remediating and improving our existing code, we treat it as a nuisance only focusing on what's next.

However new, shiny code doesn't really matter if you are reading this, and if you are running a full-fledged DevOps practice you will quickly realise that there is so much work fo do when it comes to introducing Supply Chain Management in an organisation. If you are using GitHub then great, Dependabot gives you a great headstart by integrating with the platform and continuously scanning your code. However, what if you use _something else_?

There are so many tools on the market for this: Whitesource, Snyk, etc. Even SonarQube can do Software Composition Analysis (another name for Supply Chain Management) via an [OWASP plugin](https://github.com/dependency-check/dependency-check-sonar-plugin). It goes to show how important this topic is and how much choice there is if you want to make things right.

The reason why it is really important is because your _legacy code_ is most likely running in production. Like the vast majority of us, I have a number of repositories with legacy code. This sample application was written in .NET Core 1.1, and it's been last updated in October 2017. If you never ran anything like Snyk or Whitesource, you will naturally find something akin to this state.

![](/images/posts/2022-04-06_21-18-49.png)

![](/images/posts/2022-04-06_21-16-46.png)

Some of these vulnerabilities can be easily fixed by a version bump, however others would require a complete runtime change, a migration, etc. A Supply Chain Management tool combined with your Engineering Platform will go a long way in making sure that your organisation remains sustainable.

Personally, I really like [Snyk](https://snyk.io). I used all of the tools above for years, and as of today it is the one that in my view gives the most comprehensive experience with the least amount of friction. You can set it up in minutes, and if you are targeting Azure DevOps it gives you so much power directly into the platform.

![](/images/posts/2022-04-06_21-23-56.png)

I really found beneficial having an easy way of raising Pull Requests from outside Team Projects so that development teams can benefit from them. It is also quite smart in understanding what can be easily fixed and what can't, as well as giving you so much information about the issues at hand:

![](/images/posts/2022-04-06_21-26-38.png)

In my case above there is little point in raising a PR this way, however with more recent systems it provides you with an easy way of approaching a remediation without involving too intensive efforts. Of course every time you look at something running in production you might not be able to just update the code dependencies, but that's a story for another day...