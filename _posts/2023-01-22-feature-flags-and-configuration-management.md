---
layout: post
title: Feature flags and configuration management - are they the same?
tags: [devops, architecture]
---
Recently I've been dabbling with Azure App Configuration - a very nice technology if you ask me, which allows you to build your applications or services leveraging dynamic exposure control, canary releases, etc.

I liked it so much that I spoke about that at the [London Microsoft DevOps Meetup](https://www.youtube.com/watch?v=NGoXTtnWOn0) this month, with lots of follow-up questions. One of them was pretty tough!

> Do you consider feature toggles and flags part of configuration management?

The answer is a strong yes. Feature flags, rings, etc. all rely on configuration items being retrieved. 

![](/images/posts/2023-01-22_18-33-03.png)

It doesn't really matter what they _are_...it's very much up to you what you use them for: static consumption, environment setup, exposure segmentation. We briefly talked about how to get started with adoption - rather than getting started with a massive refactoring exercise, you can slap a `legacy` flag on everything already in production, and start building new segmented areas of your application. Or you can start extracting key values used by your application (a configuration string perhaps?) and move them to Azure App Configuration so you can control their lifecycle in an easier fashion.

What really matters though is the concept of having a centralised database for configuration values. It gives you more control on a single source of truth for key information used by your services, and you can also update that as part of your CI/CD pipelines in a structured way, without relying on files. 

Extensions ([1](https://marketplace.visualstudio.com/items?itemName=AzureAppConfiguration.azure-app-configuration-task), [2](https://marketplace.visualstudio.com/items?itemName=AzureAppConfiguration.azure-app-configuration-task-push)) for Azure DevOps and [GitHub](https://github.com/marketplace/actions/azure-app-configuration-sync) make this very easy, and [`azure appconfig`](https://learn.microsoft.com/en-us/cli/azure/appconfig?view=azure-cli-latest) is the cli tool to use. 

