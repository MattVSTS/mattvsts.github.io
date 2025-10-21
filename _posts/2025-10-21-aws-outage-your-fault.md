---
layout: post
title: If you are down because of the AWS outage, it's your fault
tags: [Cloud]
---
So... your systems went down yesterday because of the outage on the `US-East-1` region. Global impact, massive problem, I agree.

Now, dear organisation... it's all your fault. **Especially** if you claim to be _cloud-native_ because you use a hyperscaler.

## Why?
Because I saw far too many instances of organisations turning down the right decision, the right design, the right implementation that takes a multi-region implementation seriously.

You had the option of enabling geo-distribution, using regional replication, designing around Availabilty Zones, anything that gave you true multi-region resiliency, and yet you didn't. The reason? 

> It's too expensive

## The business impact of penny-pinching on your Opex
Let me be super clear on this: if you use a hyperscaler as you would use a datacentre, you are not cloud-native. You are just running a more expensive datacentre without a hardware amortisation plan.

You might be benefiting from the elasticity of the Public Cloud, moving from Capex to Opex, however you have to stick to a financial envelope designed for on-premise kit. So you end-up penny-pinching.

Not using the real HADR features of Public Cloud. Faking a highly available design that just accounts for component or system failure rather than geographic or catastrophic failure. The list goes on and on...

## Change your risk modelling
You need to accept that using a hyperscaler requires a radically different approach to architecture design, risk modelling and financial estimation. 

Besides the mindset shift required in technology, think about how much risk is actually palatable... 

> If a region goes down, so does your business. Can you accept being **fully offline** for a variable amount of time?

SLAs are pointless if they are your only certainty in terms of resilience. Model your risk mitigation based on this answer to start with, and use the Public Cloud as it's supposed intended to be used if you want to be a true digital organisation.