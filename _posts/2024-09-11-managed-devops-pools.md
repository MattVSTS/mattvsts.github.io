---
layout: post
title: Simplifying Build Farms with Managed DevOps Pools for Azure DevOps
tags: [devops]
---
Over the course of my career I spent a lot of time optimising and automating Build Farms, since Team Foundation Server 2008. I remember the first time I saw the first bits of what are now Pipelines as Code at the MVP Summit as well as when I had access to an early alpha version just after Christmas a fair few years ago...shipping has always been at the core of what I've done.

Needless to say, I worked on substantial Build Farms, including replicating the seamless experience Hosted Build Agents provide in my clients' cloud estates. A lot of effort went into creating and customising Virtual Machine Scale Sets, Kubernetes clusters, Packer images, etc.  

However if you don't want to do that and you need to have _your own_ Build Farm... the answer is Managed DevOps Pools. I spent some time working on them and I am pretty impressed.

### First configuration
I ran through the Azure Portal to have an idea of how to configure a MDP and what level of flexibility you have, and it's a lot.

![](/images/posts/20240911.8.png)

To begin with, you have a dependency with Dev Center but that's about it. Very interestingly, you can configure the Agent size right away and you can select either the Microsoft images, Marketplace images or (most importantly!) your Azure images.

![](/images/posts/20240911.2.png)

The next crucial item is your Pool behaviour. These Azure resources will be deployed in a secure Microsoft subscription, and will be exclusively for you. However these will incur cost if not used, so you have a lot of flexibility in defining your behaviours:

![](/images/posts/20240911.3.png)

There is a lot of flexibility here, and we will cover this in the next section. Now onto the next big thing...

![](/images/posts/20240911.4.png)

I cannot stress **enough** how much of a big deal this is. Dealing with the infrastructure requirements of network-injected Agents deployed at runtime with finicky DNS configurations (and more) is more often than not a significant headache to setup. MDP does this for you, seamlessly.

You can then select an additional data disk if needed:

![](/images/posts/20240911.5.png)

Then you can start looking at how to connect this with Azure DevOps. It is really interesting. First of all, you can potentially share a Managed DevOps Pool with multiple organisations, if you want. You can also restrict provisioning and access to specific Team Projects. But most importantly, you can inherit permissions from the Team Project saving a lot of configuration effort if your Azure DevOps Organisation is following best practices. Brilliant.

![](/images/posts/20240911.6.png)

### My recommendations
You are still operating within the confines of an Azure subscription, so you cannot deploy a sheer amount of resources without having a high-enough quota for the SKU of VMs you want to run. If you disregard this, you will quickly end up with this error:

![](/images/posts/20240911.7.png)

Do an exercise of right-sizing, and understand if and how many agents you can warm-up to keep your teams efficient. It is your infrastructure after all, albeit deployed in a different subscription. You will be billed for it eventually!

I would also recommend against leaving Standby Agent mode off coupled with with fresh agents at least during office hours (or your peak usage window), as it will add 2-5 minutes to the provisioning of each and every agent used for the execution of your jobs. Of course it enables significant savings in terms of consumption, but unless you are using these agents for very specific circumstances (e.g.: updating production, multi-tenant environments in audited releases with a strict Single Responsibility Principle enforced) there is little benefit in that and performance will suffer.

Compared to your Build Pools, you won't have custom capabilities raised directly by your Agent into a Managed Build Pool. What you can do is set environments variables in your Custom Image, but you need to account for that when you build it, so it's not straightforward.