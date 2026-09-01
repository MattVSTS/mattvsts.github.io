---
layout: post
title: My summer project, aka Backstage on Azure in a box
tags: [open source]
---
One of the things I noticed over the years is how unnatural and sometimes convoluted Backstage is, especially for someone with a .NET development and Azure background. If you look around for an easy way to spin-up an environment on Azure you will mostly be met with either outdated, unmaintained or unnecessary resources (Backstage on AKS for a quick spin? Seriously?). So I decided to make it my summer project: build a simple demo environment in a box for Backstage.

Armed with some time and the power of various LLMs, I started trying to figure out how to remove all the friction from the process and create a way to deploy Backstage reliably and automatically so I could actually allow people to focus on the things that really matter on the platform.

This is how [Backstage on Azure in a box](https://github.com/matteoemili/backstage-on-azure-in-a-box) comes to life. It's not special nor fancy, however it's an easy way of getting an instance up and running quickly and, most importantly, using my favourite Azure service: App Service.

It is inspired by an existing open source project that gave me the immediate building blocks for what I needed. Simple infrastructure architecture and a working result. This was however completely redesigned because of my allergy to verbose DSLs (Pulumi in JavaScript just causes me a headache 😀) and I added a fair bit of scripting for automatic deployment.

The design is ever-so-slightly opinionated, as in:

- the instance will be deployed with pre-configured authentication entrypoints so you can quickly connect either GitHub or Entra for your IAM purposes.
- TechRadar is already installed, and it's currently pointing at an Azure DevOps organisation. You can easily change that if needed.
- the instance assumes the Backstage assets to be stored in Azure DevOps (and potentially GitHub).
- there is one dedicated script for granting Key Vault Secrets Officer role if needed, as by default the account deploying the infrastructure will not have the ability of browsing the Key Bault content directly. The script uses `login-hint` so you can use a federated personal Microsoft account if needed.

Of course with all the caveats of not using this in production etc., however if you want to kick the tyres of Backstage in the Microsoft ecosystem this is very much for you. Enjoy.