---
layout: post
title: Importing pipelines when the root pipeline has not been imported
tags: [pipelines]
---
I ran into this interesting bug the other day - let's say this is our repository:

![](/images/posts/2020-08-30_09-57-19.png)

All I wanted to do was importing the ```console.yml``` pipeline in Azure Pipelines. Well, I quickly learned that if you do not ever import the ```azure-pipelines.yml``` file first you are not going to be allowed to do that:

![](/images/posts/2020-08-30_10-00-17.png)

![](/images/posts/2020-08-30_10-01-15.png)

![](/images/posts/2020-08-30_10-02-00.png)

There is a way around this though - if you use the Classic Editor you will be able to point the import process at an existing YAML pipeline.

![](/images/posts/2020-08-30_10-04-28.png)

![](/images/posts/2020-08-30_10-05-08.png)

Nifty little bug, hopefully it will be fixed soon.