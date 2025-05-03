---
layout: post
title: Infusing AI in Azure DevOps
tags: [platform, ai]
---
I lost count of how many people come to me asking for AI features in Azure DevOps, and then seeing being surprised when I tell them that it's _actually_ possible to have an AI-enhanced experience with the platform. So this post brings a couple of examples to the table to try and settle the argument once and for all 😀

### The AI model
In order to start, all you need is an OpenAI model - I use mine in Azure because it's handy and convenient for me, especially for platform integrations. You an obviously use other hosting options, and that will introduce more custom work. However it's all fairly reproducible everywhere.

I deployed a GPT-4 model, and I will be using it for two specific use cases: an AI Peer Reviewer for Pull Requests and a Custom Copilot. 

The first use case is really simple, as all it's doing is really just replying to specific prompts with payload data. The second one is more interesting, as it requires adding your own information to the model. Let's have a look.

### AI Peer Reviewer
There are several extensions in the Marketplace for GPT-powered review, however the majority of them are forked from [this one](https://marketplace.visualstudio.com/items?itemName=mustaphalarhrouch.GPTPullRequestReview). I like [this particular one](https://marketplace.visualstudio.com/items?itemName=97Saundersj.AIPullRequestReview&targetId=f48ed84a-f011-41dd-a100-78d49cf2ca38&utm_source=vstsproduct&utm_medium=ExtHubManageList) because it gives me the ability to customise the prompt used as input without having to build my own custom extension should I want to do that. This is particularly important if you want to tailor the prompt for specific rules or for larger enterprise usage.

This is what you need to add to your pipeline:

![](/images/posts/2025-05-03-17-02-56.png)

Remember to use the `API_VERSION` parameter correctly when configuring the extension - use the API Version shown in the endpoint demo in the AI Foundry and you will be fine.

The result is quite nice - you have an AI Peer Reviewer in your Azure Repos Pull Request!

![](/images/posts//2025-05-03-17-13-29.png)

### Custom Copilot, like GitHub Enterprise
This is quite brilliant as it requires little effort in proportion to what you will achieve. GitHub Copilot Enterprise has a feature called Copilot knowledge bases - essentially a Custom Copilot for your documentation:

![](/images/posts/2025-05-03-17-21-20.png)

Why not having the same in Azure DevOps?

![](/images/posts/2025-05-03-18-21-30.png)

![](/images/posts/2025-05-03-18-22-12.png)

This requires a little more work: you obviously need to have Wikis in Markdown for your project(s), and then you need to upload them to an Azure Storage Account. If you want to get started quickly, just upload your Wiki content via an `AzureFileCopy` task in a pipeline. Once you do that, you can ingest the aggregated content in your model, enabling _your own Enterprise Copilot_.

![](/images/posts/2025-05-03-18-26-57.png)

It's all it takes, given Azure OpenAI supports `.md` files natively.

### How a pet project graduates to capability
The features themselves are fairly easy to craft and implement. If you want to make them robust enough for your organisation, you will need to use two things:

- A coherent documentation strategy
- Extensive usage of Pipeline Decorators

The first one is super important. You can have different file types at a stretch (look out on the [documentation](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/use-your-data?tabs=web-pages%2Ccopilot#data-formats-and-file-types)) however you really need to have a comprehensive coverage of your documentation to make this scale at organisational size, and you need to make sure you can regularly export them. Hence why Azure DevOps Wikis are so handy for this - chances are you already have all your documentation in Markdown there, so a regular export will do the trick.

For the second one, [Pipeline Decorators](https://learn.microsoft.com/en-us/azure/devops/extend/develop/add-pipeline-decorator?view=azure-devops) take away the effort required to make this a compliance requirement. 

Decorators will deploy what you need in every CI/CD pipeline. What you need is to inject a pre-job decorator that uploads the content of the repository to the Storage Account used by the OpenAI Model, and a post-job decorator that adds your chosen extension for GPT-powered code review with an execution condition similar to the one I used in the example above (`and(variables['Build.Reason'], 'Pull Request')`). 

Taking care of these two things will make your Azure DevOps AI-infused with minimal effort. 

### What else can you do? 
Can you do more? Absolutely. It all relies on adding data to the model, so exporting Release Notes, Test Reports, BOMs, even Work Items will give you more data to work with. And as you can see it's easier than it sounds.