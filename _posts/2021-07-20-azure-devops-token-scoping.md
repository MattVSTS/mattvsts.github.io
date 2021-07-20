---
layout: post
title: Azure DevOps Token Scoping
tags: [repos, pipeline]
---
Working for a client that does large scale enterprise development **and** Inner Source means we run into this fairly often with new projects consuming different `resources` in a pipeline:

![](/images/posts/2021-07-20_17-14-08.png)

It is a well documented behaviour - it's down to how Azure DevOps authorises consumption when there are permissions in place. In a nutshell, it's all down to this setting, in either the Team Project or the Organisation:

![](/images/posts/2021-07-20_17-16-53.png)

Now, why does it happen? The reason is pretty simple - every pipeline is authorised with a dedicated token, and on first run it needs an explicit validation if the above settings are on.

## What is best practice?
The answer to which is the best approach to use here is the classic _it depends_. Do you want any user in your Azure DevOps organisation to be able to get to any repository with a `checkout` step? If so disabling the settings above might be the best possible option.

Are you working with multiple parties where you need actual segregation? Enforce them at organisational level in that case.