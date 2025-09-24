---
layout: post
title: Moving from vibe coding to Agentic Engineering
tags: [GenAI, Agentic]
---
Vibe coding is great. There, I said it.

You know how much I like GitHub Copilot, GitHub Spark and all the other GenAI tools that allow someone like me, somewhat removed from being on the front row of development action, to actually be really relevant by quickly scaffolding and, eventually, creating new working code that solves someone else's problem.

Now... it's all very nice and well, but it does not work at large scale and it does not work in structured environments where variance is frowned upon and adherence to best practices and standards is vital for code to be shipped to production.

And that's the way it should be in order to avoid piles and piles of technical debt from accumulating in your codebase. What if I wanted to leverage AI to do more than just scaffolding, and drastically accelerate my SDLC?

## Spec-driven Development
The answer is [`spec-kit`](https://github.com/github/spec-kit), a lightweight framework that translates specifications into individual chunks of work that can be delegated to one or more Agent.

This is a particularly sensitive topic in enterprise environments: as of today you had to craft your prompts very carefully otherwise risking a disconnect between your requirements and the code being produced. This is no more.

## How does it work?
You install Specify and you setup a project with `spec-kit`:

![](/images/posts/2025-09-24-15-45-32.png)

You will have three additional commands for GitHub Copilot in Visual Studio Code:

![](/images/posts/2025-09-24-15-47-32.png)

These are the three fundamental commands of SDD - it follows a _why-what-how_ paradigm:

- Why = **Specify** the vision
- What = **Plan** the technical implementation
- How = Break down the specification into actual **Tasks**

They will live off a file called `constitution.md`, which acts as the immutable principles upon which the commands will run, and most importantly, is the de-facto **memory** for your key commands:

![](/images/posts/2025-09-24-16-21-21.png)

Before diving into details, keep in mind that every command template lives in the `.github/prompts` folder, they are Markdown wrappers towards the `specify` CLI to be used by GitHub Copilot (or your favourite assistant) and everything can be customised and extended as needed, so these are effectively templates.

### Specify
`/specify` will read your requirement and generate a detailed breakdown of your acceptance criteria, the sub-features and components of the requirement, and every functional detail required for a solid implementation.

![](/images/posts/2025-09-24-15-57-32.png)

This _specification_ is the functional understanding of the requirement from the GenAI perspective:

![](/images/posts/2025-09-24-16-04-03.png)

Your quality gates will be an explicit part of the specification:

![](/images/posts/2025-09-24-16-11-59.png)

### Plan
`/plan` is the command to be supplied with the technical details of the implementation you want the Agent to follow, so it can generate an execution plan for your Agents:

![](/images/posts/2025-09-24-16-13-52.png)

![](/images/posts/2025-09-24-16-22-52.png)

Something really interesting here: the _constitution_ is enforced at plan time:

![](/images/posts/2025-09-24-16-24-17.png)

That's why that file is central to the whole idea of SDD.

### Tasks
Once you are ready to proceed, you can generate the task breakdown:

![](/images/posts/2025-09-24-16-25-14.png)

You will get an interesting list of tasks that can be given to one or more agents:

![](/images/posts/2025-09-24-16-25-51.png)

Here you can add or define any key dependency, library, etc. to remark to the agents for implementation.

### Implement
As a first timer, I wanted to observe how the tasks were implemented (you can run `/implement` otherwise), so I manually triggered the execution in GitHub Copilot Agent Mode:

![](/images/posts/2025-09-24-16-36-33.png)

It was really interesting to observe the iterations and how it tried to solve problems, including with running tools:

![](/images/posts/2025-09-24-16-37-31.png)

It took a while...

![](/images/posts/2025-09-24-16-43-28.png)

And eventually, it delivered:

![](/images/posts/2025-09-24-16-40-12.png)

And yes, it actually works 😀

![](/images/posts/2025-09-24-16-48-41.png)

## So what?
The key difference between vibe coding and agentic engineering is the repeatability of a solution. The key foundation of Agentic Engineering is giving developers more time to focus on the actual value-added, rather than diluting their flow state with repetitive and sometimes tedious activities.

For this to happen, developers need to be coordinating a number of agentic processes so that they can then review and augment what is otherwise machine-generated code to the expected standard.

Spec-driven Development bridges that gap today, giving teams a way of exploiting all the power of GenAI for developers without having to manually keep an eye out for every single execution. It's quite literally at the frontier of our industry, I could not more excited for future developments!