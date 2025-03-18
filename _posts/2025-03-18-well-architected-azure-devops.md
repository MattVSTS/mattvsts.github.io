---
layout: post
title: How about a Well-Architected (Framework) for Azure DevOps?
tags: [platform]
---
Someone asked me the other day:

> You blogged about GitHub Well-Architected, it's brilliant. Why is there no Azure DevOps equivalent?

Fair question, and I will try (and surely fail!) to keep the answer short.

### Azure DevOps is different
Simply put, Azure DevOps is designed with a logical container (Team Project) segregating a slice of all the services available on the platform. Team Projects have always beem used to define _Projects_ and store all the data related to them in a single place.

You always had code repositories in there, a representation for time (Iterations, to be defined in days) and space (Areas, representing logical subsection of your work). Everything is designed around these concepts.

This also affected the level of access control, which is super granular and allows custom roles to slice and dice access (or visibility) as needed.

### Historically there wasn't much consideration for this
Bit of a history lesson over here, with the customary nostalgic tear 🥲. Azure DevOps is based off a product called Team Foundation Server.  

All the content sat on a single database for the longest time. Starting from Team Foundation Server 2010, Microsoft introduced the concept of _Team Project Collections_, and it started splitting up data storage. Git was not an option until Team Foundation Server 2012, everything was stored in a centralised Version Control System before then.

Between Team Foundation Server 2010 and 2012 is also where the codebase was forked to develop TFSOnline, which became Visual Studio Online, which became Visual Studio Team Services, which eventually became Azure DevOps Services.

### One Team Project to rule them all
After so many years, we needed to move away from what we called "[TFSGuide](https://www.amazon.co.uk/Development-Visual-Studio®-Foundation-Server/dp/0735625719)" (TFSGuide was the name of the file and the alias to send feedbacks to...) and onto something that was more industrialised. TFSGuide was a large collection of SOPs and designs every ALM consultant knew almost by heart.

This is where we started defining new best practices, which ultimately resulted in the "One Team Project to rule them all" approach. This is still very much the best practice, as Microsoft continues to update [documentation](https://learn.microsoft.com/en-us/azure/devops/user-guide/plan-your-azure-devops-org-structure?view=azure-devops#how-many-projects-do-you-need) on this. 

It is in essence - everything in a single Team Project, as many code repositories, groups, teams, areas and iterations as you need based on your logical structure (teams, squads, products, CoPs, etc.). It works well and it's considered the golden standard unless you absolutely need to keep things segregated.

There is one exception though, besides the segregation example above. You remember how much I like Pipelines as a [dedicated serverless environment](https://mattvsts.github.io/2024/04/22/engineering-ingenuity-will-always-prevail/) for platform automations, right? Let's just say _Two Team Projects to rule them all_ then 😀
