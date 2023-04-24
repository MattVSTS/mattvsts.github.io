---
layout: post
title: No more excuses with App Registrations in Azure DevOps
tags: [azure devops]
---
It's not really news, however...you can now [add](https://learn.microsoft.com/en-us/azure/devops/integrate/get-started/authentication/service-principal-managed-identity?view=azure-devops) App Registrations and Managed Identities as users in Azure DevOps.

![](/images/posts/2023-04-24_20-53-14.png)

They will cost you a licence, however there is one massive benefit in enterprise environments: you can stop manually managing Personal Access Tokens, and you single-handedly control granular access to your environment(s) via a single identity.

This is a game-changer, as you can finally stop spending time on handling PATs (monitoring them, sending reminders to owners, etc.) as well as worrying about unfettered access that might leak via a misused token.  

Also, this also means you can now control anything in ~Azure Active Directory~ Entra and you can guarantee unattended or privileged access to singular entities with a single Service Principals in a bidirectional fashion on environments and organization.

Imagine...

> An App Registration is the only identity allowed to perform operations more privileged than just Read, directly connected to Azure DevOps and completely managed in Entra.

This, for enterprise environments, is massive. 