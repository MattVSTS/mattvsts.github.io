---
layout: post
title: Solving an identity crisis in an Azure and DevOps world
tags: [security, PAT, platform]
---
So... _identities_. A cornerstone of any cloud platform and essential in a DevOps world. However I end up talking about these on a daily basis in the Azure space, so I hope this post can act as a cheat sheat for my readers! One disclaimer though: I am not an identity expert, so I might use some simplification here and there.

## Where it gets messy
There are two kind of identities we are interested in: interactive and unattended. 

The problem users face is that one of these two categories is actually more complex than it should be - the unattended one. There are several distinctions to make, however let's clear out what _identities_ are first...

## Interactive v unattended
As you may guess, an interactive identity is anything associated to an actual user: _name.surname@tenant.com_, _DOMAIN\namesurname_, or anything else that refers back to an actual carbon-based life form (sorry Andy, it makes me chuckle every time!).

The same is true for something like a PAT token in Azure DevOps too. Yes, it's a token rather than a _username+password_ combination, however it still brings authentication back to an interactive user, hence it is an interactive user.

It's worth remembering that these are the worst type of users to deal with in a hyperautomated setup, and you should not try to use them in any form of automation unless absolutely necessary. Passwords will expire, 2FA will kick-in, etc. They are unreliable when it comes to automatic interactions.

An unattended identity is anything that is registered in the directory system however it doesn't necessarily expose a password, and it is still part of the Role Based Access Control model that ~any cloud provider~ Azure uses.

## Managed Identities
A Managed Identity is a resource type in Azure. You can create a user-assigned Managed Identity or a system-assigned Managed Identity.

The difference between the two is in the lifecycle - a user-assigned one is a standalone resource type, and you physically control it. Unless you delete it, it exists. You can assign it to different resources, and explicitly group together multiple resources with it. 

A system-assigned Managed Identity instead is unique to, and tied to the resource it's part of - once the resource is deleted, the Identity goes too.

## Application Registations and Enterprise Applications
This is the most common identity-related question I reply to all the time - argh!

> What is an Enterprise Application?  
> How about an Application Registration?  
> Isn't it a Service Principal?  

So, let's make it clear - all of these live in Azure Active Directory.

An Enterprise Application is...an application. Any application registered in AAD, from **any tenant**. Azure DevOps? Enterprise Application. ServiceNow? Enterprise Application. Teams? Enterprise Application. It's an entity that represents an application across one or multiple AAD tenants.

An Application Registration is the representation of an application you **own** (yours, custom) in Active Directory. It's also tied to an Enterprise Application - because it is an application. 

The difference? The Application Registration contains all the application settings (authentication, secrets, API permissions, etc.), while the Enterprise Application is used for RBAC and it is the actual entity used for authentication.

## What is a Service Principal?
Service Principals are often used as synonyms for Application Registrations (because that's where the keys/secrets/passwords are), however it is wrong. The Service Principal is hosted in the Enterprise Application, and it is what you actually use for permissions.

The confusion is annoying though - let's say you create a Service Connection in Azure DevOps. What happens there?

![](/images/posts/2022-02-28_22-14-02.png)

Ah, it says Service Principal! Brilliant, that's it then! Even the link says that!

![](/images/posts/2022-02-28_22-15-04.png)

However if you click that link you will end-up in an Application Registration blade of the Azure Portal.  

![](/images/posts/2022-02-28_22-17-11.png)

The Application Registration and the Enterprise Application will have the same Application ID, however different Object ID in Active Directory. 

![](/images/posts/2022-02-28_22-19-18.png)

They are two entities for the same thing.

## What do I use in DevOps?
All of them. Managed Identities represent resources, Enterprise Applications any form of service or application requiring an identification and an Application Registration is what you use to generate secrets and contexts of applications you own.