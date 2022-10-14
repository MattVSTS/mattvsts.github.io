---
layout: post
title: Defender for DevOps, or rather enterprise integration...
tags: [devops]
---
Great news at Ignite in the past few days. There is one I am particularly close to: [Defender for DevOps](https://www.microsoft.com/en-us/security/business/cloud-security/microsoft-defender-devops).

There are a number of reasons I am excited for it, there is no denying! The most important one is because Defender for DevOps makes your development platform (either Azure DevOps or GitHub) front and centre when it comes to security integration with the rest of the organisation.

Let me explain: unless tightly integrated, development platforms tend to drift away from enterprise governance - shifting left is twice as hard if nobody outside the engineering department has got visibility of it. That's when the complex integration journeys begin, products start popping up with no coherent vision, patched together by either custom code or flaky tools. Doing things right in this space is possible, however it's harder and it requires way more guidance at a strategic level.

Enter Defender for DevOps - this is all it takes to get going:

![](/images/posts/2022-10-14_22-12-45.png)

![](/images/posts/2022-10-14_21-15-07.png)

You will need to authorise Defender via a Project Collection Administrator account:

![](/images/posts/2022-10-14_21-15-28.png)

![](/images/posts/2022-10-14_21-15-35.png)

And you will be done:

![](/images/posts/2022-10-14_21-15-50.png)

Now, a word of advice. Defender for DevOps is extremely dependent on the tenant the Azure DevOps organisation is connected to, and it is also a preview so a few niggles are to be expected.. 
If the tenants are not aligned, Defender will never be able to find the target organization, so bear it in mind when it comes to multi-tenant situations.

Should you ever need to switch tenant for an Azure DevOps organization, you can do that under the Azure Active Directory tab in the organisation settings, with the **Switch Directory** button. It is seamless, nothing is lost if the tenants are configured correctly:

![](/images/posts/2022-10-14_21-30-37.png)

The end result will be something like this:

![](/images/posts/2022-10-14_21-34-50.png)

The organisation is now connected and it will be populated. All is left to do now is to install the [Microsoft Security DevOps extension](https://marketplace.visualstudio.com/items?itemName=ms-securitydevops.microsoft-security-devops-azdevops), and you can start adding the relevant task (`MicrosoftSecurityDevOps@1`) to the pipelines you are interested in. Results!

![](/images/posts/2022-10-14_21-54-41.png)

There is obviously more to do and more potential features to use, however this gives you an idea of why I believe it is so important. It also opens the door to a unified Azure DevOps and GitHub developer platform for enterprise organizations - the steps to configure Defender are the same, all it changes is the use of a GitHub App rather than an Azure DevOps identity.
