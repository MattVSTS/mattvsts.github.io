---
layout: post
title: The key difference between vertical and horizontal GenAI assistance
tags: [GenAI, Copilot]
---
I answer this question at least once a week so I will use this as a more permanent signpost 🙂

> _What is the difference between GitHub Copilot and Claude Code/OpenAI Codex (or any other vertically-integrated GenAI assistants)?_

The answer might be simple, however there are a couple of nuances to think of. Let's have a look.

### Model availability
This is the obvious one, and we kind of [talked about it](https://mattvsts.github.io/2025/12/06/choice-model-matters/) in the past. With GitHub Copilot you have a choice of models you are not going to get with other tools. 

Do you want to mix models from different providers? It's a selection on a dropdown menu. This flexibility is not available with other providers, and will give you the opportunity to switch, chop and change models as you see fit based on the best experience you get.

It is a very personal choice in the end, and it's a unique selling point of a horizontal GenAI assistance.

### Workflow integration
In the IDE, the experience is different remarkably different between the two. 

GitHub Copilot is a hands-on assistant, which is very available in your environment no matter which mode you are going to use it with. Most of the experience is centered by default on the single developer, and puts severe importance on context.

Code completion, inline generation, etc. are all typical use cases for developer augmentation, where having the tool accelerates the unitary task being worked on. Agents can be local or cloud-hosted, however they run in relative proximity to your work even if you delegate tasks to them, as you need to be very prescriptive with the context you provide them. 

GitHub Copilot is also heavily integrated with the GitHub platform, and it's a unique team advantage. It's like getting additional capacity out of a magic hat for specific tasks like Pull Request reviews and security remediation via Autofix.

On the other hand, any vertically-integrated tool has a remarkably different paradigm: even if they might be available in the IDE, they put a lot of effort in repo-wide context and CLI accessibility. They work against the whole repository building a context independently, and the agentic experience is way more delegated and hands-off compared to GitHub Copilot. 

When I work with Claude Code for example, it is still very developer-centric however delegation is more wide-ranging. The CLI is the most powerful tool to use with it and it has high context awareness. 

OpenAI Codex has an even stronger delegation system and runs mostly asynchronously, it's very task-based and gives its best when performing isolated, wide-ranging implementations or tasks, so the IDE and the interactive experience is almost irrelevant for it.

### Is there a silver bullet?
No. 

The level of comfort with innovative ways of working and practices will obviously skew things one way or the other. Platform integration might or might not play a part at all. Repository availability and solution convention can be disruptive either way. There is no clear _winner_ to be had here, but just the best choice out of a very crowded field.

Much of the choice also depends on the preferred ways of working of an individual or a team, as well the governance structure in place for developers, which might limit or hamper any of these tools in an expected way. 

Eventually, one does not exclude the other. I saw organisations using both technologies for well-defined, discrete use cases and building a unique multilateral approach.

So no single winning choice (sorry!) but rather lots to think about in your own context and your own organisation. 