---
layout: post
title: A reflection on the risks of GenAI
tags: [GenAI]
---
Earlier this week, Anthropic shared [details](https://www.anthropic.com/news/disrupting-AI-espionage) about how a hacking group used Claude for a highly sophisticated espionage campaign against a number of organisations. 

This obviously sparked a number of conversations around the topic of security of GenAI tools for developers, and I ended-up explaining to some of our clients that even if they wanted to add their own security process and vetting (pointless, we'll see why) they wouldn't be able to do anything with the same speed and efficiency as Anthropic.

This begs the question though... what can an organisation do, realistically, about it?

### Accept that complete prevention is not possible 
When you are introducing a GenAI-driven tool you must accept a degree of risk. Risk is, specifically, around the speed of execution for malicious intent coming directly from within. Let's have a look at an example: if you ask GenAI to help you with something, it will really try to help you if you use a somewhat advanced model (Claude Sonnet 4.5 here):

![](/images/posts/2025-11-15-20-33-09.png)

Note the latter stage of this: "...**_let me create a quick start script_**". This is not a simple ask-iterate-execute loop, but rather a full-blown reasoning cycle which leads to unexpected actions. In this case the example is positive, the tool created a whole script to aid with a certain piece of work, but it begs the question: can you restrict this? Short and definitive answer: no.

When I say no, I mean without restricting unnecessarily all the valuable functionalities that you get with more advanced models. Realistically, do you believe you can do _better_ than your supplier?

Microsoft, GitHub, Amazon, Anthropic... they all perform extensive testing before releasing models for consumption on their platforms. GitHub talks about it [here](https://github.blog/ai-and-ml/generative-ai/how-we-evaluate-models-for-github-copilot/), covering their AI model evaluation process, and if something is released on their platforms is incredibly unlikely you would be able to find something they didn't.

Also, this is a service. If this was your own model you could run something like [`modelbench`](https://github.com/mlcommons/modelbench), however you have to implicitly accept the risk as you cannot really do much more than they do, given you are just a downstream consumer.

### Some things don't really change
What I always bring up to CTOs, is that the risk here is not new. You have a new vector, not a new threat in itself. The [full report](https://assets.anthropic.com/m/ec212e6566a0d47/original/Disrupting-the-first-reported-AI-orchestrated-cyber-espionage-campaign.pdf) is a very interesting read, as the way Claude ended-up being used was to speed-up ~~hacking productivity~~ tactical execution work (sorry 😆) and it was heavily reliant on jailbreaking and rogue MCP servers.

The jailbreaking process is novel, as it managed to bypass the safety guardrail Anthropic setup on the model. That's the core issue, and they moved very quickly.

Whilst you can't do anything about jailbreaking (that's a supplier-managed guardrail and Anthropic already fixed the pattern), what you can do is control MCP servers and, obviously, monitor the environments from where activities are carried out. Nothing that a good, old SOC can't do, and it will still be linked to one or more users via network traffic.