---
layout: post
title: Inner Source in an enterprise, the contribution model
tags: [innersource]
---
Finally the most important topic to cover: how to build a sustainable contribution model?

Inner Source is not just some code dropped somewhere so that anyone can use it. Inner Source is about enabling teams to evolve their codebases in an organic fashion, ensuring reuse and synergies wherever possible.

## Decision making

Decision making is very simple in Inner Source: everything is transparent, automatic processes ensure quality, your governance is enforced by design and the consumers naturally align with the objectives of the project. The maintainer team will always be the one dealing with the vision and its transformation into execution, however every Inner Source project will always be transparent because everything happens in pure openness, for everyone.

In order to do that you need a usable process that allows anyone to get their changes to the main codebase without an excessive amount of friction.

> Pull Requests!

You might suggest Pull Requests. Yes, they are part and parcel of the process, but before you get there you need a few extra items along the way. Also remember how documentation plays a key part, because it's where you define the ground rules: branching strategy, baseline testing, rules for documentation, etc.

## The importance of a package

What are you trying to achieve, exactly? In my past [post](https://mattvsts.github.io/2022/09/27/innersource-enterprise-consumption/) I mentioned how important it is to make the end user experience simple enough so they can get going quickly.  
If you want to do it you need to define what is your _package_, the artifact that the users will consume. It can be a repository, it can be a binary, anything will do as long as it is consumable.

Your package (or its content) will need to be versioned in predictable way. Semantic Versioning usually comes to the rescue, however you can also use a simpler version with just `Major.minor` as values. What really matters is using it right: it will be your contract with the consumers, so make sure to setup some solid ground rules as well as documentation to support that. 

In my latest Inner Source project I settled on a code repository as a package, containing a number of versioned items. With the right documentation in tow users can use it in a simple and straightforward way, easily embedding it into their projects while at the same time ensuring upgrades remain seamless due to the nature of the repository.

## Testing
Testing will be the most important step to establish when it comes to Inner Source contributions. Yes, there might be a test suite in the codebase, however you need to enforce its execution, together with some extra scans ensuring your quality levels.

The other side of the coin is that everything must be automated, no matter what. There is absolutely no reason for your quality bar to rrely on human intervention. If you cannot automate things, don't do Inner Source or it will suck so much time out of your day.

I say that seriously: an Inner Source product (being open by default) requires a lot of attention, as much if not more than a traditional project, and it really needs a strong set of automations to remain smooth and lightweight. With every contribution there is a new opportunity, however there is also a sizeable risk of overseeing critical stuff. Automate your processes.

## Am I mature enough for it?
Inner Source doesn't happen overnight - it's something that takes time to evolve, like every cultural change, you might try and fail a few times, however it's not necessarily down to a single team or organisation. You might have full organisational backing and no contributors, or many contributors with no outlet for converging. 

Remember to setup a vision for it. It can be speed, it can be reuse of code, it can be collaboration. As long as you have something you are striving for, Inner Source will help your organisation achieve it with the power of decades of Open Source development. 

It is a mindset change that requires exercise and the right balance in place, otherwise it will quickly become overhead.