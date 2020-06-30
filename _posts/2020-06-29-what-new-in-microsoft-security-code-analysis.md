---
layout: post
title: What's new in Microsoft Security Code Analysis?
tags: [pipelines, security]
---
I blogged about the toolkit in [the](https://mattvsts.github.io/2019/11/01/when-to-integrate-sca/) [past](https://mattvsts.github.io/2019/10/22/getting-started-with-sca/), Microsoft Security Code Analysis is something that you should look at if you want to integrate a solid set of static code analysis procedures around the security space.  

Over the past couple of months the team released a major set of [enhancements](https://docs.microsoft.com/en-us/azure/security/develop/security-code-analysis-releases), and it is clear that there is still so much coming through to properly implement security scans in Azure DevOps.

## CredScan updates
Aside from being 25% faster, CredScan can now identify new secret types, including various types of access tokens. This was a long-requested feature, because not all passwords are a username and password combination and having the capability of automatically detecting these is extremely important. You definitely do not want an Azure Active Directory access token in the clear into your repository!

## Futures
There a few interesting items in the roadmap: analysers for Java, Python and Azure Resource Manager templates. These not only expand the language selection, but they will also cover Infrastructure as Code files, making it a foundational tool you can integrate not only for .NET code, but also for other languages.