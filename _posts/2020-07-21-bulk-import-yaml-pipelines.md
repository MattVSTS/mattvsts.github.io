---
layout: post
title: Bulk import YAML pipelines in Azure DevOps
tags: [pipelines]
---
If you import or fork a repository with many YAML pipelines you will soon face this issue...

> How can I import all these pipelines?

Doing it manually would be quite tedious, so you should use the APIs. Or, even better, the Azure DevOps CLI!

Assuming you are going to get a list of paths in a standard format, you can run this simple PowerShell script from a local copy of your Git repository...

```
$pipelines = <your paths/pipelines/names/etc - something to uniquely identify your pipelines>

foreach ($p in $pipelines){
    az pipelines create --name $p --description "Pipeline for $p" --repository <your clone URL> --branch <branch> --folder-path <folder destination for pipelines> --yaml-path <the path where $p is> --skip-run
}
```
As simple as this is, it is quite a valuable script.   
Given a source of standard paths or pipeline names (you need to build it as you like), it is going to create new pipelines importing the existing YAML files, sorting them into the destination folders you like in Azure Pipelines and skipping the initial run so you are not going to overwhelm your agent pool.