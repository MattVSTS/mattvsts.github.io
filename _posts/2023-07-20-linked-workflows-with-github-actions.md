---
layout: post
title: Linked workflows with GitHub Actions
tags: [github actions]
---
This is literally the simplest possible thing, however... I wanted a workflow to be triggered only on successful execution of another workflow in GitHub Actions. I thought it will take somewhat more than the single `workflow_run` [keyword](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_run)!

It is one of the many triggeres available under the `on:` condition, and it will link one or many workflows to a secondary workflow. Beware, it does not act as a logical AND.

I put together a simple example on my account, [here](https://github.com/MattVSTS/Linked-Workflows), I hope this helps. It helped me, given I wanted exactly that feature!