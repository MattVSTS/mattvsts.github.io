---
layout: post
title: Inner Source in an enterprise, the role of testing
tags: [innersource]
---
Driving back home tonight I thought it was about time I continued my series on Inner Source... now time to talk about testing.
It is part of the model you must define for contributors as well as embedding it within the validation process the team will enforce. Let's see how.

## Testing for contributors
Demand extensive testing as part of your contributions. Testing must be both effortless and extensive, there is no getting around to that.  
If a contribution is not thoroughly tested, it will automatically fail the validation process no matter what.  

How would you define "testing"? Well, first of all you need to test the literal functionality you are delivering.  
Unit testing, assertion-based testing, anything that defines how a single feature is tested is absolutely a must. The hard part comes when you need to test integration with other features or parts of the system. In case of an application, typical integration testing works fine - however consider scenario-based or environment-based testing in order to ensure the contribution doesn't break any existing functionality. If you are running other forms of testing, remember to ensure they are clearly separated from each other.

## Automating testing to validate contributions
This is where things get interesting - once your contribution is tested, it needs to be tested again during the review process. So it becomes about _how_ rather than _what_.
You need to ensure end-to-end execution without requiring a single finger being lifted - for all of the tests above. Running them as part of your build validation is key. And it takes time.

When designing a testing strategy for your product this is the second thing that will take most of your time (the consumption model would be the top one). If testing isn't seamless, you lose out on contributions. If testing is excessive, the result would be the same.

It's not necessarily about _how long_ it takes to test, but rather _how much effort it takes_ for someone to run end-to-end and deep testing suites. Getting this right will enable a lot of contributions.

