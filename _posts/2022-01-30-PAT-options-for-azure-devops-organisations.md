---
layout: post
title: PAT options for Azure DevOps organisations
tags: [security, PAT, platform]
---
This was a fairly unknown feature, however it's a very important one when it comes to security in a large-scale Azure DevOps deployment...

As I am sure you know, PAT tokens are secrets directly bound to an identity - user-managed, easy to consume and very valuable for automations (we'll talk more about all things identity in the short future). These tokens represent a user, and they can be scoped to the most granular level of access. What unfortunately happens though, is that users will create a full-scope Access Token for the sake of convenience - often with the longest expiration possible.

This is an incredibly poor security stance, as secrets can leak and they can be a major risk. However I was really please to find out that Azure DevOps allows you to configure three key options at an organisation level:

- Enforcing an organisation to scope the PAT onto
- Enforcing a specific scope rather than Full Access
- Enforcing a defined lifespan

These three policies are really easy to configure yet so powerful - you can enable them, and also provide a whitelisted set of users and groups to exclude, for any reason you might have.

![](/images/posts/2022-01-30_16-27-39.png)

It's worth mentioning that some APIs are not consumable if you are not using a full-scoped PAT. Microsoft clearly calls this out in their [documentation](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/manage-pats-with-policies-for-administrators?view=azure-devops), and hopefully they will provide a list so you know when to whitelist a user.



