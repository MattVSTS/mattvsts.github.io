---
layout: post
title: Hey, my Service Principal expired!
tags: [azure, platform]
---
If you used Azure DevOps long enough, you will eventually run into a situation like this - your Service Principal will expire and throw this error:

![](images/posts/2019-08-19-20-55-34.png)

![](images/posts/2019-08-19-20-51-22.png)

Don't panic if you see this - when you authorise an Azure Resource Manager Service Connection Azure DevOps creates a new App Registration in Azure Active Directory (even if you are using as public tenant like hotmail - you will still get an AAD tenant to use):

![](/images/posts/2019-08-19-20-38-35.png)

This App Registration has a default expiration of two years:

![](/images/posts/2019-08-19-20-39-30.png)

The error simply means that your Service Principal expired. All you have to do is to renew the Service Principal **from the Azure DevOps UI** and you will be good to go. Don't renew it from the Portal, as otherwise Azure DevOps won't know how to handle the secret!
