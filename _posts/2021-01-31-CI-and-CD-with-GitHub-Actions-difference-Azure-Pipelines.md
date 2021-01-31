---
layout: post
title: CI and CD with GitHub Actions - what is different from Azure Pipelines?
tags: [pipelines, actions]
---
Eventually, I did it - I tried an end-to-end CI/CD workflow exclusively on GitHub Actions. Talking about details, I moved my end-to-end demo of an ASP.NET Core application deployed to an Azure Web App (with Deployment Slots), with MSDeploy packaging and infrastructure deployment via Azure Resource Manager.

Nothing really complex or bleeding edge, but susprisingly commonplace in many organisations. It was neither difficult nor totally plain-saling, so I thought about putting together what I found interesting. If you need one takeaway though, it better be this: YAML is an investment for you. The sooner you are comfortable with it, the sooner you can tackle pretty much anything!

## Look into the environment variables before you start
Like Azure Pipelines, GitHub Actions has its own set of [environment variables](https://docs.github.com/en/actions/reference/environment-variables). Look into them and make sure it's all clear for you - you'll need them!

One to remember: ```GITHUB_WORKSPACE```. It is the folder where your repository is downloaded! In order to use that you need to surround it like that:

{% raw %}
```yml
...
    template: ${{ github.workspace }}/src/IaC/template.json
...
```
{% endraw %}

## GitHub Actions is an agnostic platform
GitHub Actions does not have any specific connection or accelerator to any target platform. While this is a big advantage in several situations, it can take you off-guard if you try to move from an orchestrator with service connections like Azure Pipelines.

If you like me are targeting Azure, you are going to use the [Azure Login](https://github.com/marketplace/actions/azure-login) action all the time, and you need to setup one or more dedicated Service Principals in advance so you can actually interact with your tenant.  

{% raw %}
```yml
    - name: Subscription Login
      uses: azure/login@v1
      with:
        creds: ${{ secrets.<your secret name> }}
```
{% endraw %}

Once you have a Service Principal you need to store it - I recommend to create an environment secret, as this is scoped to the target environment like the name suggests. These are encrypted within the GitHub platform, but they cannot be linked to something like Azure Key Vault. You can also use an organisational secret, if you want to share them across multiple repos or environments, but I would rather use permission scoping wherever possible!

## No templates or stages in GitHub Actions
There are no templates in GitHub Actions, plain and simple - this leads to little reuse if you don't plan it well in advance. Looking at the public [roadmap](https://github.com/github/roadmap/projects/1?card_filter_query=templates), they are targeting Q2 2021 for [centrally managed templates](https://github.com/github/roadmap/issues/98) and an undefined future for [private templates](https://github.com/github/roadmap/issues/51) as in Azure Pipelines.

![](/images/posts/2021-01-31_15-22-39.png)

There is also no real concept of _stage_ in GitHub Actions. Your stages will be separate YAML files, and you can invoke them as needed. It's just different.

## You require a deeper knowledge of what you are targeting
If you use Azure Pipelines, every time you add a task you can inspect anything related to it via the Task Assistant in your editor, so even if you don't know all about it you can get an idea about what you can do with it:

![](/images/posts/2021-01-31_15-07-18.png)

The closest you can get to that is looking at the GitHub Marketplace listing and at the examples contained in there:

![](/images/posts/2021-01-31_15-13-39.png)

![](/images/posts/2021-01-31_15-14-23.png)

It's a different approach - more control at the cost of being less intuitive.

## Running a workflow manually is not as simple as it should be
GitHub Actions is a platform orchestrator that _happens to do CI/CD_. There is no such thing as a _manual run_, so you need to add this snippet to your ```on``` condition:

```yml
on:
...
  workflow_dispatch:
    inputs:
      logLevel:
        description: 'Log level'     
        required: true
        default: 'warning'
```

This will enable the relative UI:

![](/images/posts/2021-01-31_15-35-19.png)

It's not out-of-the-box and you need to know what to change - I hope it will become simpler in the future. Sometimes you need to run a workflow manually, and you don't want to pollute your commit history with whitespace changes...