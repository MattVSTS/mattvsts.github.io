---
layout: post
title: Enforce governance on Azure DevOps Organisations
tags: [platform, azure]
---
This is a crucial but often overlooked detail when it comes to corporate adoption of Azure DevOps - how can I prevent users from creating _rogue Organisations_?

Needless to say, the first port of call would be to understand why the _rogue Organisation_ was created in the first place. Talking to each other goes a long way! And more often than not, the underlying reason is a simple misunderstanding of requirements or a lack of communication betweem two parties. The main reason why Organisations should not proliferate is because it can easily become a governance nightmare - especially when you start connecting Azure subscriptions. 

While there is always a chance of someone creating an org with their own personal Microsoft Account (nothing you can do about that I'm afraid!), we have some options to track or even prevent Organisations created with AAD backing but without approval.

The reactive route is fairly easy to implement: you can setup an Azure Monitor Alert looking for operations against the _Microsoft.VisualStudio/Account_ Resource Type:

![](/images/posts/2019-11-20-15-18-51.png)

This will alert you if someone creates a new Organisation connected to an Azure Active Directory tenant. It is good, but it is still reactive: someone did it and now you have to fix it.

The proactive way has just been released - the documentation is [here](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/azure-ad-tenant-policy-restrict-org-creation?view=azure-devops), and the role looks like this:

![](/images/posts/2019-11-20-15-19-56.png)

The new Administrator Role, that is going to contain a list of authorised users, is combined with a feature which ties-in with your existing Azure DevOps Organisations:

![](/images/posts/2019-11-20-15-13-42.png)

These two together prevent the creation of unauthorised AAD-backed Organisations, and simply the overall governance of the stack. Fewer operations to worry about!