---
layout: post
title: Build a Custom Copilot Chat command in seconds
tags: [Copilot]
---
A simple yet underrated way of accelerating standardisation in an enterprise engineering platform is to build custom Copilot instructions to bundle in your repositories.

Whilst that is very true, we should not just think of them as overarching, standard prompts that give custom information to our developers. That would be true of a `copilot-instructions.md` file in the root of the repository, however anyone can develop their own, just by adding a `<command>.prompt.md` file in the `.github/prompts` folder.

Something like this:

![](/images/posts/2025-09-17-13-11-17.png)

You will be able to invoke it from the `/pirate` command in Copilot Chat:

![](/images/posts/2025-09-17-13-13-11.png)

This would invoke the prompt (_"can you help?"_) with my pre-defined context setup for the command:

![](/images/posts/2025-09-17-13-21-37.png)

And it will result in... well, exactly what you'd expect 😂

![](/images/posts/2025-09-17-13-15-29.png)

It's not magic, it's not special, it's just part of the GitHub Copilot infrastructure in Visual Studio Code, that allows you to [create](https://docs.github.com/en/enterprise-cloud@latest/copilot/how-tos/configure-custom-instructions/add-repository-instructions) custom instructions. 

Obviously, being a Markdown-based approach, you can also use it in your coding agents if you have something specific in them - all you have to do is to refer to them as part of your Agent prompt.

