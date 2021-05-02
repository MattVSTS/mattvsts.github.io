---
layout: post
title: Just roll-up your backlogs!
tags: [agile]
---
I know - it's 2021 and Agile methodologies should be used as standard. They are, for the most part, but every now and then I find myself talking to clients that would like to see a proliferation of _projects_ (Team Projects in Azure DevOps if you like) to keep their teams in the dark about their peers, while at the same time they want to have a portfolio-level view of everything happening at any given time.

> I want a pretty cake, I want to devour it, and I want the cake to remain pretty.

That is not just a pipe dream, but it's rather wrong too. Think about it: do you want to move in the direction of obscure boundaries with teams, whilst the whole industry is going in the opposite direction?

The answer is no, of course. These questions are not intentionally malicious - to the contrary, it's just a reflection of the comfort zone of an organisation. Moving on is always feasible (being willing of course), and more often than not once _the new normal_ is demonstrated people are very keen to get on with it.

Take the above example: team focus and portfolio management at the same time. How can you do that, effectively, and with minimal friction?

Take Azure DevOps for example. Don't create a sprawling mass of Team Projects in an organisation. Unless you have regulatory reasons to keep things physically separate (and even then, we should still have a chat), you can easily live with a single Team Project.

All it takes is a couple of settings to iron out to get what you want:

- the org-level team will contain all your individual teams (and each individual team will have an Area assigned to them)
- set the org-level Areas setting to include all the subareas from the root one

Job done. Each team will be able to access their backlog, as well as being able to link their work to the shared Features/Epics that you use for shared priorities. This also enables [Delivery Plans](https://devblogs.microsoft.com/devops/delivery-plans-2-0-is-now-ga/) to be easily created, and portfolio management becomes a manageable task without introducing friction.

Why complicate things if all you need is already out there? Elegance and pragmatism always go a long way.