---
layout: post
title: What is the difference between Defender for DevOps and GitHub Advanced Security?
tags: [devops]
---
Very interesting question the other day:

> What is the difference between Defender for DevOps and GitHub Advanced Security?

The answer is simple yet not clear-cut. Let me get there.

### Defender for DevOps
Defender for DevOps is part of Azure Defender - the Cloud Security Posture Management tool for Azure and beyond. It can connect with GitHub and Azure DevOps repositories, and it provides code scanning vulnerabilities, security exposure alerts and supply chain management capabilities.

### GitHub Advanced Security
Regardless of the target platform (GitHub or Azure DevOps), GitHub Advanced Security is a tool designed to integrate with your development platform and help your developers shift security left. It provides code scanning vulnerabilities, security exposure alerts and supply chain management capabilities.

### The key difference
Defender for DevOps operates outside-in. It will inspect your codebases, it will raise alerts and will provide recommentations. It is designed to provide data points to consume at enterprise platform level.

GitHub Advanced Security does the same, however tightly integrated with the development platform, meaning you can integrate it with your development workflows. It is not just a surfacing and aggregation tool - it also provides proactive help to the developers.

### An example
A developer tries to commit an Azure Storage Account SAS Key into the Git repository. 

Defender for Cloud will only identify it after it goes through a CI/CD pipeline which uses the `CredScan` task (so the leak will be contained to the code repo and the platform admins or owners will receive an alert), GitHub Advanced Security will simply not allow you to commit the secret.