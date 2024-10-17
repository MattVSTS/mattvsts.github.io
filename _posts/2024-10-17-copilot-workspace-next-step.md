---
layout: post
title: GitHub Copilot Workspace is the true next step in the SDLC
tags: [github]
---
### Supercharging GitHub Copilot
Copilot here, Copilot there... yes, GitHub (and others!) Copilot is brilliant, but it only acts as a sidecar support to the developer experience. You will see a lot of productivity improvement, and you will have a much happier developer population, but it will be fundamentally linked to the team size and the organisation.

This is where things get interesting - Agents are the next logical step in a GenAI adoption journey. Agents are able to perform operations independently from the user, under supervision, leading to a precise outcome. They significantly help augmenting a capability, and are going to become prevalent in the next few years.

GitHub Copilot Workspace gives you Agents you can use to significantly grow what your development teams are doing. I think it's a game changer.

### An example
Let's start with a controlled example: a starter application created with `dotnet new mvc`. Nothing special, nothing fancy, but assume for now that this is your existing codebase you are working with.

I am going to ask Copilot Workspace to implement a CI pipeline in GitHub Actions based on the code at hand:

![](/images/posts/20241017.1.png)

This is where the true power of Workspace shines:

![](/images/posts/20241017.2.png)

Copilot Workspace "understands" (it's a LLM, it has no reasoning, but it can interpret things based on context as we know) what we are working with and what we need to do. It will generate a number of steps:

![](/images/posts/20241017.3.png)

Each of these steps is going to be linked to changes to the code:

![](/images/posts/20241017.4.png)
![](/images/posts/20241017.5.png)

If I am happy with it, I can open a Pull Request against a branch. This will contain the work done by Copilot Workspace:

![](/images/posts/20241017.6.png)

Now... I might want more. Let's ask Workspace again:

![](/images/posts/20241017.7.png)

I noticed the packaging step created by the agent is not what I want though, as I get an error in my CI workflow:

![](/images/posts/20241017.8.png)

I can change it by asking again on the prompt box or by editing the file myself, and it will do what I need with the right level of information:

![](/images/posts/20241017.9.png)

Now, this is a simple example. Imagine doing this with explorative branches, codebase explanation, etc.

You now have an Agent which can work independently on relatively complex requests, and you can steer its outputs with a few prompts. 

### The key difference 
Why is it different? Copilot Workspace will break down a prompt into multiple actions, within the same context. So you don't get a bounded code generation, but rather a series of independent actions which will achieve a complex outcome. 

Agents can live independently as sessions, and you will always be able to track back or initiate new ones from the Development Platform. They are an extremely powerful tool for development teams to significantly improve the impact they can deliver against their backlog!

The industry is significantly changing, and tools like Workspace were unthinkable even a few yearsa ago. I am looking forward to seeing what else Copilot Workspace will be able to do within GitHub Enterprise!