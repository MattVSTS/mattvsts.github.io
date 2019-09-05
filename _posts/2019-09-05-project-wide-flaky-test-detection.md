---
layout: post
title: Project-wide flaky test detection
tags: [testing]
---
Azure DevOps is a complex platform and today I found out something quite interesting: [system-wide flaky test detection](https://docs.microsoft.com/en-us/azure/devops/pipelines/test/flaky-test-management?view=azure-devops).

A really neat feature indeed - you can configure detection and management of flaky (unreliable) tests so that it does not affect the overall statistics of your code quality analysis.

![](/images/posts/2019-09-05-16-33-15.png)

In my opinion this feature shines when your tests are under development, and they are not yet finalised in your codebase. With it you can have a reliable picture with the stable tests as part of the test reporting side of the build, and these tests under development will be left _on the side_ to allow for analysis and fixes.

Of course you have total control over what is recognised as Flaky/UnFlaky, as per this documentation screenshot:

![](https://docs.microsoft.com/en-us/azure/devops/pipelines/test/_img/flaky-test-management/mark-flaky-1.png)

You can always change the category and alter the build result.