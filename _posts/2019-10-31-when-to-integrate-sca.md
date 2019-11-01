---
layout: post
title: When to integrate SCA?
tags: [DevSecOps, pipelines]
---
As much as I am a fan of [Microsoft Secure Code Analysis](https://secdevtools.azurewebsites.net/) I would not go and blindly integrate the whole suite without a degree of thought.

If you attended one of the sessions where I talk about quality, as part of my common sense approach to blending security concepts into the DevOps fabric of an organisation I still swear by nimbleness and agility - meaning I am not going to transform a 30 seconds build into an ordeal. We are in luck with SCA though, as most of the tools bear a minimal overhead so we can integrate as many as possible into a CI build!

That said, still think wisely about how you are going to implement the toolkit: stuff like CredScan or BinSkim should always be integrated in a CI build. BinSkim slows things down a little bit, but the benefit of that is that every binary vulnerability will be raised immediately rather than after a PR or a merge. It is worth it - you don't want to spend more time fixing a develop build!

On the other hand a full-blown malware scan (maybe with a boot sector scan as well), with a large set of artifacts can take a long time and you might not want to run it in a regular run-of-the-mill build. The place where this is mostly needed is towards the final stages, where you are preparing these bits for consumption.

The _Roslyn Analysers_ and _TSLint_ are very much an extension of what you can do in your IDE (more to come on that) and the overhead is similar to a local build - the impact varies massively depending on the rules you decide to apply. It's a call you make on the balance of things, and you have alternatives like SonarQube that can help swing the decision.