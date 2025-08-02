---
layout: post
title: The current state of Agentic Engineering with GitHub Copilot
tags: [AI]
---
2025 is all about AI with agents, and as always developers are at the forefront. There are layers to it though, and I keep getting confused clients approaching me about some of the possibilities. At the end of the day this is not just about tools, and Agentic Engineering is not about giving all your developers access to GitHub Copilot or Amazon Q Developer, but rather a cohesive approach to the end to end lifecycle.

We looked at a few things [here](https://mattvsts.github.io/2025/05/03/infusing-ai-in-azure-devops/), but these are just tooling examples. Let's try to broaden the subject and summarise where we are as an industry point of view.

### Assistants like GitHub Copilot are a commodity
As I said earlier, access to GitHub Copilot does not make your engineering organisation AI-native. In 2025 we should be well past the point of _proving value_ for a rollout, yet I still talk to clients about it on a daily basis. 
Access to GitHub Copilot (or any other developer assistant) is table stakes if innovation is the top priority, and if you are not doing it, rest assured your competitors are. 
Costs are negligible compared to the value returned, the ability of giving developers an immediate boost pays for itself and there are huge positive implications - essentially every active measurement survey proves that, in each and every rollout I am involved in, so sample size is not one.

There are different ways a developer gets benefits from using GenAI, and it will ultimately depend by the way you use it. Regardless, it is a no-brainer. 

### Supporting developers
A developer is supported by GitHub Copilot when they use it in the IDE, regardless of the mode.

Code completion, Ask Mode, code generation and Agent Mode are all aimed at augmenting the work our teams do so they can add their specific skills and knowledge in the most efficient way, with every tedious, repetitive or otherwise time-consuming operation out of the way.

An example of this is Agent Mode. Copilot does something for your developer, but still their your direct supervision:

![](/images/posts/2025-08-01-10-16-07.png)

Supervision here is key: with Agent Mode your continuous feedback loop ensures the output is what you actually need. This is not an agent working in unattended fashion:

![](/images/posts/2025-08-01-10-18-28.png)

The immediate impact of using Agent Mode is that developers work on their codebase with significant acceleration, more than just using code completion or generation, and with tangible efficiency benefits.

### Augmenting developers
Augmentation for developers is evident when a developer is able to scale significantly using Coding Agents.

A Coding Agent is real, unattended delivery where the developer only reviews, leaving the actual implementation to the agent itself. A developer can then start their flow on something else, and once the agent is done they can review, comment, and suggest changes. Look at this example:

![](/images/posts/2025-08-01-11-00-07.png)

This is a super crude user story. There is little context, zero information about NFRs, only a goal outlined: write the Unit Tests against a codebase. Yet, once I assigned it to a Coding Agent, it did that and more:

![](/images/posts/2025-08-02-14-41-32.png)

The interesting thing is that a Coding Agent can and will understand failure and remediation:

![](/images/posts/2025-08-01-11-18-59.png)

The way it works is simple: the Agent analyses the context from scratch, and it uses the whole repository. 

![](/images/posts/2025-08-01-11-21-07.png)

That's how it can understand _the whole thing_ and delivers the functionality in roughly 15 minutes and you can still interact with it in a PR to trigger further work:

![](/images/posts/2025-08-01-11-27-57.png)

It could obviously be much more efficient as well, with custom instructions, environment setup or other features, but more on that in a future post 🙂.

Developer augmentation is not just pure feature generation: you can (and should) leverage Copilot Agents for code review as well, directly in your Pull Requests:

![](/images/posts/2025-08-01-11-27-02.png)

These two use cases alone are the foundation of Agentic Engineering.

### What's next?
The biggest difference with other tools or platform is that Agentic Engineering keeps evolving. Today we talk about GitHub Copilot Coding Agents, but Claude Code (to name an example) is emerging at breakneck speed and something else might come up next week or the week after.

Things will also go beyond the pure coding aspect of the developer workflow, [Copilot Spaces](https://github.blog/changelog/2025-05-29-introducing-copilot-spaces-a-new-way-to-work-with-code-and-context/) is an excellent example. Think of it as shared context analysis for small scale (PBI, bug fix) implementations. It's a brilliant brainstorming aid and it helps shifting left some of the effort required in a Pull Request.

Ultimately the goal for Agentic Engineering is to settle on practices and approaches where the platform works on your behalf and the developers can express multiples of their potential. Ideally, the platform should be something multimodel and extensible. GitHub Copilot is, frankly, both - so it is perfect ground for future developments. I am excited for what's next!
