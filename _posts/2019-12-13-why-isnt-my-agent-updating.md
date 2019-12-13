---
layout: post
title: Why isn't my agent updating?
tags: [pipelines]
---
This happens fairly often in restricted configurations where there are proxies, firewalls, etc...
Let's say you want to update your Azure Pipelines agent from the UI:

![](/images/posts/2019-12-13_17-06-00.png)

If you see a message saying that it's downloading the agent and then goes back to Idle, chances are you have a networking issue on the agent machine, usually towards the internet.

The agent update process is fully automated, and all it does is downloading the new agent from a well known address (https://vstsagentpackage.azureedge.net), and replacing the binaries.

Go and have a look in the Agent log:

![](/images/posts/2019-12-13-17-11-00.png)

You can see that the machine cannot download the new agent package, hence the process fails and releases the agent from the lock to bring it back to the pool. It's a totally safe operation, but you won't see any error message surfacing in the UI by design.