---
layout: post
title: Template extensions in Azure Pipelines
tags: [pipelines]
---
As part of a project I am working on we have a strong usage of Pipelines templates, and the consumption chain is nested across multiple repositories.

In my situation, let's say we have a ```Core``` repository, that contains a set of baseline assets. There will be another repository in a ```Department``` Team Project, aggregating multiple assets from ```Core``` and offering them as _templates_ for broader consumption. Which will bring you to a ```Consumer``` which will use these _templates_ (and potentially do more things).

The first step is very easy: you define your ```asset.yml``` pipeline in the ```Core``` Team Project, which does a number of things. 
That pipeline is then invoked by a ```template.yml``` in the ```Department``` Team Project:

```yml
resources:
  repositories:
    - repository: Assets
      type: git
      name: 'Core/Core'

steps:
- template: asset.yml@Assets
  parameters:
    param: ["a", "b"]
```

This is pretty straightforward. But what if you want to consume your ```template.yml``` elsewhere, as a nested template? You cannot do the same as between ```Core``` and ```Department```, because it will complain about the pipeline being invalid with an _unexpected ```resources``` value_.

The answer is in the ```extends``` keyword: it allows a template to be used as-is, and extended as needed:

```yml
resources:
  repositories:
    - repository: Templates
      type: git
      name: 'Department/Department'

extends:
  template: template.yml@Templates
```

With that I am going to be able to consume the templates in the way I expected.