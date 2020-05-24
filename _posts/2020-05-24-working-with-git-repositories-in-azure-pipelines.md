---
layout: post
title: Working with Git repositories in Azure Pipelines
tags: [repos, pipelines, github]
---
I keep talking about [Azure Pipelines](https://www.youtube.com/watch?v=hgLzCQArWEA) a lot these days and there are so many features in the Pipelines as Code implementation you just miss or overlook because you cannot go around the UI, poking stuff, turning dials and seeing what happens. At least, that's what I always do :-)

This time around I want to spend some time on what you can do with Git repositories in Azure Pipelines, because once you start embracing Pipelines as Code there is so much you can do with them - regardless of your versioning approach (single or multiple repositories).

## Working with multiple Git repositories
One of these features is multi-repository access, and it gives you so much power over the handling of repositories as part of a pipeline run.

Reaching out to multiple repositories, within a Pipeline is very simple, by leveraging the appropriate _Resources_ keyword and checking-out the repository you are interested in - it can be hosted anywhere, as long as it is reachable via a Service Connection:

```
resources:
  repositories:
  - repository: ExternalRepository
    type: github
    endpoint: GHEC
    name: Org/Repo
...
steps:
- checkout: ExternalRepository
...
```

What if you want to specify a repository at runtime, rather than as part of the definition? If that repository is contained in your Azure DevOps Organisation (anywhere!) you can just run this as part of your steps, replacing the stuff within brackets:

```
steps:
...
- checkout: git://<Team Project>/<repository name>
...
```

You can also choose the branch you want to checkout, by adding a _ref_ property to the repository resource or appending _@<your branch ref> to the checkout step:

```
resources:
  repositories:
  - repository: ExternalRepository
    type: github
    endpoint: GHEC
    name: Org/Repo
    ref: develop
...
```
```
steps:
...
- checkout: git://<Team Project>/<repository name>@develop
...
```
One typical example of multiple repository access is when you have a repository containing your Pipeline templates, and you need to run some of them as part of your specialised pipeline run, contained in a different repository (a microservice, for example). It's as simple as this...
```
...
steps:
  - template: templates/my-template.yml@ExternalRepository
...
```
## Trigger filtering for branches and Pull Requests
Yes, when you create a pipeline you get a CI trigger on master by default. But it is just the beginning...
```
trigger:
  branches:
    include:
    - master
    - develop
    - feature/*
    exclude:
    - experimental/*
  paths:
    include:
    - '/'
    exclude:
    - 'docs/'
    - 'assets/'
```
This example runs a certain pipeline on a CI basis only when a change is pushed to master, develop or any feature branch. It explicitly excludes experimental branches, and changes to the docs/ and assets/ folders. No fiddling around with comboboxes or toggles, you just type it down like this.

If you are using Azure Repos, then the Pull Request trigger is going to be handled by a Branch Policy and you should not do anything to your Pipeline definition. If you are using any other Git hosting platform, then you can copy the code above and replace the _trigger_ keyword with _pr_ to implement a trigger filter for PRs as well.