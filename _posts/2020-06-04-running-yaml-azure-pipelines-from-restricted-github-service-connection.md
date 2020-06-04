---
layout: post
title: Running YAML Azure Pipelines from a restricted GitHub Service Connection
tags: [repos, pipelines, github]
---
Last week a colleague (hi Kapil!) ran into an interesting scenario:

> what if I can't use the GitHub app to integrate Azure Pipelines with my GitHub repository? All I have is a GitHub PAT.

The target GitHub repository contains the YAML Pipeline definitions, but it has no visibility towards Azure DevOps. All you have on the Azure DevOps side is a Service Connection created with a PAT.  
This is a situation where the GitHub organisation restricts access to external parties, so they only release a PAT to allow for controlled access. It's not an optimal situation IMHO, but we should make it work regardless.

If you choose the Azure Pipeline classic editor, you will be able to consume that Service Connection:

![](/images/posts/2020-06-04_11-02-03.png)

You will be surprised to discover that once you point it at the right source (your GitHub Service Connection mentioned above), you will have an option to use a YAML file:

![](/images/posts/2020-06-04_11-09-56.png)

All you then have to do is to set the path to your YAML definition, and the two will be integrated:

![](/images/posts/2020-06-04_11-11-58.png)

![](/images/posts/2020-06-04_11-12-59.png)