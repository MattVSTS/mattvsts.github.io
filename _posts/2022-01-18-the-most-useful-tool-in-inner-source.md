---
layout: post
title: The most useful tool in Inner Source
tags: [github, repos, git, innersource]
---
I introduced Inner Source to my current client roughly 18 months ago. It was a big change for a massive 100,000 employees organisation, used to somewhat traditional development practices (not Waterfall - I would have flatout refused!) however quite curious and willing to try out innovative ideas.

The journey continues uninterrupted, there is always so much going on and the contributions are quite steady - Azure DevOps really shines with Boards, and teams are fully onboard.

There is however one tool (if you want to call it as such...) that really helped us along the way. It's not a technology tool, a stack, or even a script, but something rather simpler...

### Immutable commits
Defining immutable commits is like defining a package. You know what it is, what it contains, its version. We however work with Git repositories, so the definition becomes cloudy: what would be your _package_? Adding further complexity to the question, we ship a _product_ available to everyone inside the organisation, and the contribution model needs to fit a Git consumption scenario quite easily. 

In our case we settled on the hash of the commit. It's the option with the lowest friction, and it is a common denominator for everyone. The idea is simple: if you want to contribute something, you work in your own fork. There you can develop however you like (within the framework), however you need to end up in a situation where you have unique commits to push. This is accomplished by Pull Requests.

These commits are then pushed to the main repository, where they get integrated and eventually made available to the  consumers. Simple, right?

### The idea behind it
While now the core development team works on the main repository themselves, contributors need to ensure they are not pushing commits with `duiqsrbf0quibwri0pufb` as a commit message (or worse!). We also need them to clearly label what they are pushing, and this helps a lot in narrowing down issues down the line.

Let's take this as an example:

![](/images/posts/2022-01-18_18-33-11.png)

These can all be external contributions. How? Well, like this:

![](/images/posts/2022-01-18_18-35-57.png)

The commit hashes are the same across the board, despite being different repositories and different team projects altogether! What really matters is that `Core.Department2` ended up pushing a bunch of validated, reviewed commits to `Core` like packages. 

### How to put this into practice
The implementation can be achieved with any system supporting Pull Requests. When you accept any external contribution using this model you need to ensure the PRs are closed enforcing **rebase and fast-forward** as a merge strategy:

![](/images/posts/2022-01-18_18-39-37.png)

This ensures that only commits really _ready-to-go_ (imagine a staging area) can be pushed along. This also doesn't mean that you need to have one commit per PR, or duplicate effort - the name of the PR might be _Merged PR 58: Updated README.md_, however that contained the top two commits you see in the history!

![](/images/posts/2022-01-18_18-42-50.png)

### Enforce it
It's all down to good practice. Like I said, the core development team works on the repository directly so they can squash merge all the changes, while the external contributors have to go through their own fork. This is enforced via a simple Branch Policy in Azure Repos:

![](/images/posts/2022-01-18_18-45-18.png)

If you want to do the same in GitHub, you need to look at this setting in the repository Options, under Settings:

![](/images/posts/2022-01-18_18-51-00.png)

Finally, we used to have the core development team follow the same process as the contributors for over a year. Same game, same rules for everyone. The reason why we moved away from it was simply down to the volume of changes and features delivered, making it slightly impractical. 

If, however, the difference in volume is not massive or there is no core development team then I would recommend going for the same standard across the various teams and remove the squash merge option.