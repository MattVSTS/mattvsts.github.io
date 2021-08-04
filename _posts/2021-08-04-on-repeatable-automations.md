---
layout: post
title: On repeatable automations
tags: [automations, pipelines, actions]
---
> Automations are the cornerstone of DevOps, and they allow for a substantial increase in speed and quality.

I say this at least on a monthly basis, which is good because it means there is demand for adopting automations. The industry pushes towards the trend of _automating everything_, and I am sure your technical feed is no stranger to advocates of this discipline. It's great, as this momentum drives collective improvements.

What we usually do not see is, however, what comes next. You should not just _automate_, you should automate _in a repeatable fashion_. Let's take a look at how you can get there.

## Repeatable automations - what are you talking about?
An automation **must** be repeatable. An automation is not just a script. An automation is something you can run any time, and it is going to return a predictable output at all times.

Let's take an example familiar to everyone: creating a resource, whatever that is, in a Resource Group. It's a simple command at the end of the day:

```powershell
Create-MyCoolResource -ResourceGroup $resourceGroup
```

Now you want to automate it - very good. You (and I) will likely end up running something akin to:

```powershell
param(
    $resourceGroup
)
Create-MyCoolResource -ResourceGroup $resourceGroup
```

A simple input of a Resource Group name and off you go with your automation. Nice. The next logical step is to execute this command via a form of unattended environment, like inside an Azure Pipeline or a GitHub Actions workflow, possibly backed by a Service Principal. 

However, this will fail 100% of the times if you run the same command against a multi-subscription environment: if your Resource Group is not in the default subscription for the identity running it, the command will not be successful. Think about the Service Connections in Azure DevOps - they are either scoped to a default Subscription or a default Resource Group, then whatever happens behind the scenes is handled in Azure.

So what will you do here? Well, easy enough, you will add a parameter to request an explicit Subscription ID:

```powershell
param(
    $resourceGroup,
    $subscriptionId
)
Create-MyCoolResource -ResourceGroup $resourceGroup -SubscriptionId $subscriptionId
```

Doing this ensures that as long as the identity running the command is authorised, it will be able to reach the right subscription and perform `Create-MyCoolResource`. Thinking upfront about these situations requires awareness and adds very little work to an otherwise simple process, however doing it pays dividends longer term.

## Pre-empting your context and validating your inputs
Following on from the above example, how can we make sure we are covered from unexpected situations where a command will not support something like an explicit SubscriptionId parameter? It's critical to think about that scenario, because you might have to integrate your new script with some other existing code, or utilities, which _might_ not behave as expected.

Step back, and think about where you are executing this script. How do you ensure you are safe from the condition? Simple: add an explicit [context setup](https://docs.microsoft.com/en-us/powershell/module/az.accounts/set-azcontext?view=azps-6.3.0)!

```powershell
param(
    $resourceGroup,
    $subscriptionId
)

Set-AzContext -Subscription $subscriptionId

Create-MyCoolResource -ResourceGroup $resourceGroup -SubscriptionId $subscriptionId
```

This ensures that whatever you do, you are covered by the context being set at the earliest possible stage.  

Then obviously, you can do more: making your parameters mandatory and type-validated so you are prevented from entering useless inputs, as well as adding some good old [try-catch](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_try_catch_finally?view=powershell-7.1) and text outputs to make sure messages and errors are surfaced nicely:

```powershell
param(
    [Mandatory]
    [string]$resourceGroup,
    [Mandatory]
    [string]$subscriptionId
)

Set-AzContext -Subscription $subscriptionId

try {
    Create-MyCoolResource -ResourceGroup $resourceGroup -SubscriptionId $subscriptionId
    Write-Host "Resource created"
} 
catch {
    Write-Host "An error occurred"
    Write-Host $_
}
```

## Retry wherever possible
Call me biased if you like, but I am a big fan of retry logic. It's simple, and provides so much support in fully unattended situations. Retry logic acts as a safety net for networking and platform issues, ensuring your commands will be automatically rerun in the correct fashion.

In our case, how does it look like?

```powershell
param(
    [Mandatory]
    [string]$resourceGroup,
    [Mandatory]
    [string]$subscriptionId
)

Set-AzContext -Subscription $subscriptionId

$count = 0
do {
    try {
        Create-MyCoolResource -ResourceGroup $resourceGroup -SubscriptionId $subscriptionId
        Write-Host "Resource created"
        break
    } 
    catch {
        $retry++
        Write-Host "An error occurred"
        Write-Host $_
    }
} while ($retry -lt 3)
```
A very simple retry logic here re-runs the command for three times if an error is caught-up, otherwise the resource is created without further ado. This is a very powerful tool as it gives you a way of not wasting time on platform-level issues (a transient network issue can derail processes, let me tell you!) while still giving you a huge amount of control. 

You can also use this approach combined with some waiting time, so that you can actually rule out external environmental issues like service unavailability.