---
layout: post
title: Integrate Fortify in Azure DevOps, how easy!
tags: [platform, pipelines]
---
For my latest session (at [WinOps 2019](https://www.winops.org/london/agenda/computersaysno.php), brilliant conference as usual) I dabbled with some addition to my session on Code Quality and DevSecOps.

One of these additions was Fortify - a well-known security scanner from Microfocus. I played with their On-Demand offering, and I was amazed at how easy it is to setup. There were a couple of catches I want to mention though.

Bearing in mind a security scanner in a Pipeline simply sends the code samples to the service, I was expecting it to be smoother to configure. Nothing hard, undocumented or complicated, but there are a couple of things that might require clarification. 

For example, creating a BSI token. A BSI (Build Server Integration) token is something used by Fortify to identify the application and the build server used as a gateway. All is nice and good, but when I tried to configure the token directly from the Azure Pipelines suggested link I only got as far as a login error goes.

![](/images/posts/2019-09-30-21-08-52.png)

![](/images/posts/2019-09-30-21-06-54.png)

On the other hand, doing the same from the Application Dashboard worked a charm.

Also, the task itself - don't expect anything other than a green build if it all goes to plan:

![](/images/posts/2019-09-30-21-10-22.png)

There is no dashboard integration within the build or any other sign of communication between the two. That said I am not expecting CI builds to include this scanning tool so it might be understandable.

All in all the tool is very nice though. Something I particularly enjoyed is seeing the level of detail it can go. Let's take this _simple_ issue:

![](/images/posts/2019-09-30-21-12-51.png)

Not only you will get a technical explanation with a safe example, you will also get a list of all the best practices and standards (**including GDPR**) you are violating:

![](/images/posts/2019-09-30-21-13-45.png)

I reckon it is a very valuable information to have in this day and age. Just don't integrate it in the CI build (but pass it along onto master and develop) as otherwise you won't be able to appreciate its value.