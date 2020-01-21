---
layout: post
title: A closer look at the pipeline authorisation model
tags: [pipeline]
---
It all starts from this error...

![](/images/posts/2020-01-21_21-13-59.png)

Yes, you can click the button and (possibly) fix it, but what was the cause of that?

The answer is simple: every Service Connection you are going to consume within a Pipeline needs to be authorised. What usually happens is that a Service Connection is automatically authorised for the project (or even across projects), and then someone _decides_ to remove the pipeline authorisation leaving you with a red build.

Fixing this is really easy - your Service Connection has got a Security menu. Look into it...

![](/images/posts/2020-01-21_21-20-07.png)

![](/images/posts/2020-01-21_21-20-46.png)

Click on the + button to add at least a pipeline, or to grant full-fledged access across different projects:

![](/images/posts/2020-01-21_21-22-38.png)

![](/images/posts/2020-01-21_21-23-06.png)

Needless to say, you can restrict access as much as you like - play with the ACLs as much as you like, but regardless of that Pipelines and Users will have different authorisation models. Especially because Pipelines themselves are considered [resources](https://github.com/microsoft/azure-pipelines-yaml/blob/master/design/pipeline-resources.md) in the new YAML world...