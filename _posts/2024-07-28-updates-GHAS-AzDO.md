---
layout: post
title: Recent improvements in GitHub Advanced Security for Azure DevOps
tags: [security, DevOps]
---
Over the past few months a number of good updates were released on GitHub Advanced Security for Azure DevOps, I felt they went a touch under the radar! Let's see what these are, there are a few key changes worth knowing.

### Overall security overview
You now have a single pane of glass view of your security posture across the organisation, under **Organisation Settings**:

![alt text](/images/posts/20240728.1.png)

This is a quality of life improvement, however for large organisation it also allows an understanding of hotspots and coverage at a glance. Very useful!

### Enhanced secrets scanning
Secrets scanning is now enhanced, able to detect different patterns compared to the original set of vendor patterns. These are non-provider specific (e.g.: connection strings and various private keys!) and are incredibly common sights in scans.

| New Pattern |
|------------------|
ASP.NET Machine Key
DER-endcoded Private Key
Dynatrace Token
GPG Credentials
HTTP Request Headers
JavaScript Web Token
LinkedIn Credentials
MongoDB Connection String
MySQL/MariaDB Connection String
PEM-encoded Private Key
PGP Private Key
PKCS12 Formatted Private Key
PostgreSQL Connection String
Putty Private Key
RabbitMQ Credentials
RSA Private Key
SQL Server Connection String
SSH PrivateKey	OpenSshPrivateKey
SSH PrivateKey	GitHubSshPrivateKey
URL Encoded Credentials

These are in addition to the long [list](https://learn.microsoft.com/en-us/azure/devops/repos/security/github-advanced-security-secret-scanning?view=azure-devops#partner-provider-patterns) of Provider Patterns already supported.

### Automatic Agent preparation for CodeQL detection
I really like this one, especially if you roll it out in a decorator in a self-hosted Build Farm: you can now automatically setup an Agent with the CodeQL extension as part of the Initialize CodeQL task in a Pipeline:

![alt text](/images/posts/20240728.2.png)

This will save you the hassle of setting up the CodeQL tools upfront and maintaining them up to date.