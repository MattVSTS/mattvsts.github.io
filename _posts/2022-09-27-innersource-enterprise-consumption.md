---
layout: post
title: Inner Source in an enterprise, the consumption model
tags: [innersource]
---
I wanted to talk about the contribution model first, however I felt it would be important to think about the users first. So after talking about the whys, it's time to talk about one of the hows: how to consume an Inner Source project. How will your users consume your code? Why is it so important?

## Documentation is your main enabler

The barrier of entry needs to be lowest than ever. It might be a `README.md` file, a SharePoint or Confluence page, a Wiki, what really matters is that users can get going as soon as possible.

Low entry barrier doesn't mean no or little documentation. To the contrary, the more the better. What I found really intuitive is a mix of high-level, getting started documents coupled with deep, low-level pieces detailing every possible parameter, scenario or functionality. An Inner Source project is a product at heart, so it needs to be treated as such.

Consider automatic documentation generation - it makes your life so much easier. [Docs as code](https://www.writethedocs.org/guide/docs-as-code/) also ensures automatic compliance with your contribution model, making it part of a contribution. Technologies like [Jinja2](https://jinja.palletsprojects.com/en/3.1.x/) or GitHub Pages make writing documentation so much easier and straightforward. Worst case scenario, a code wiki in Azure DevOps does wonders!

## Make it easy to use
Whatever you are building, make sure to bundle an automatic build script at a minimum. Not just a detailed, step-by-step guide, but rather a one-click-script. A pipeline would be even better. You need to make sure your users will be able to get going with a single interaction, no matter what.

If you are developing code to be used alongside other code, I would strongly recommend an approach where your code repository becomes a package - doing that means that everybody will get immediate benefit from updates, and it doesn't require any form of update besides getting it. 

For example, Azure DevOps has a dedicated YAML keyword (`resources`) which allows you exactly that:

```
resources:
  repositories:
  - repository: innersource
    type: git
    name: InnerSourceProject/tool

steps:
- checkout: self
- checkout: innersource
...
```
Your pipeline automatically consumes the latest version of the Inner Source code, with no effort. Easy.

Why am I pushing so much for it? Well, it's about one of the main differences compared to Open Source development - you have a fundamentally different audience compared to the outside world.  
Yes, many people will be as passionate and engaged, however some will be less interested and maybe even _forced_ to use your tool.  Not everybody, unfortunately, cares. By making the consumption experience as seamless as possible you are removing a number of potential support questions to field, and the first contact for someone who is not necessarily excited about the codebase will as positive as it comes.

## Try to bring them along
Don't forget to include an easy way for a user to engage with the maintainer team, either to request something new or to report a bug, and if they had a smooth and easy experience chances are they would be interested in contributing and enhancing your product with their features! So ensure your documentation covers the contribution model, and you will hopefully be able to get contributions out of them!  

