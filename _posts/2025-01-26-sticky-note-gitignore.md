---
layout: post
title: A sticky note for myself - enforce a .gitignore file
tags: [git]
---
No matter how many times I do that, I keep creating new repos and adding a .gitignore file afterwards - so I need to enforce it after the fact (especially after you start bulding and you have the annoying build artifacts in your file system!).

This is literally a sticky note for myself 😃:

```bash
git rm -r --cached .
git add .
git status # to check for missed files
git commit -m 'enforced gitignore'
git push origin <branch>
```