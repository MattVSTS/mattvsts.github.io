---
layout: post
title: Inner Source in an enterprise, measurement is king
tags: [innersource]
---
Back on the topic of inner source, we now need to look at how we define _success_. Measurement and the right metrics will tell you if you are going in the right direction, and given it's an internal project this data is going to be priceless in order to understand what to do next.

## Establish a good set of metrics
The consumer is the most important persona in this scenario, so it's ever so critical to get the metrics right. Tracking everything is one thing, putting your reading glasses on and analysing this data will be another matter.

Track actual actions - a deployment being executed, an API being invoked, any material action which makes sense to collect from an interaction point of view. This excludes contributions - they would be tracked separately in the developer platform itself.

Focus on what you want to understand. Adoption comes in many ways, however ensure you can build a good view of how your product is used. 

## Track everything, only if it makes sense
Given it's an internal project we are talking about, you can take some liberties when it comes to tracking adoption. This doesn't mean collecting PIIs from your colleagues or scraping the organisation for how many times your code was cloned, but rather having a good granularity of events and interactions collected in total transparency.

It's important to avoid getting swarmed with white noise. Getting a list of all `git clone` commands your users ran against a repository (for example) doesn't make sense no matter how tempting it might sound. Someone could be cloning a repo to kick the tyres of your codebase, with no further usage. Build runners might be cloning your repo at pace because of several builds running in parallel. It is pointless.

However be systematic in tracking, user interaction data is what will elicit patterns of usage and potentially raise early signs of issues. Get good quality data.

## Learn and iterate
You surely want to know who is using your stuff, and what is not going well or causing issues to your users. That would be the most important measurement you can take.

Once you have this adoption data, iterate quickly on it. Initially you will notice a sea of anomalies and more problems than progress - this is perfectly normal, you won't get it right first time around. However over time (and Pull Requests) you will quickly be able to identify what is going as expected and what doesn't.

This picture will allow you to get a better understanding of your consumer base and how your product is being (mis)used. Early detection of these things is pivotal to proactively engage, given a critical mass. Otherwise it's all data fundamental for retrospective analysis.

