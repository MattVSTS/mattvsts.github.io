---
layout: post
title: Unpublishing your latest Git commit
tags: [repos, git]
---
Sometimes it happens - you pushed a commit to a remote repository and you need to remove it, in a rush and without changing the repository's history.

There are so many ways of doing that, but one reliable and easy way I found is this:

```
git push <remote> +<hash>^:<branch>
```

This will **force push a removal, for a commit hash, on a certain branch, of a certain remote**.  

I wrote it this way because it is very easy to explain :-) It's also easy to automate because it targets a single commit.
