---
layout: post
title: Did you know? Repo branching policies in Azure DevOps
tags: [repos]
---
It's one of these things that go unnoticed until you actually stumble upon them: did you know that Azure DevOps has a number of branch policies you can apply to each repository in your Team Project?

![](/images/posts/2019-11-13_18-40-40.png)

These are repo-wide, different than the ones specific to the single branch. I am very fond of the **Commit author email validation** one that blocks lazy people not setting up their Git Config correctly :-)

![](/images/posts/2019-11-13_18-51-04.png)

It's also very handy to be able to control the maximum file size and path length direcly:

![](/images/posts/2019-11-13_18-51-59.png)

Check them out, I am sure you will find an excellent use of these. Small details, but they can make the difference sometimes.