---
layout: post
title: How I moved my demo SonarQube server to Azure Container Instance
tags: [cloud, containers]
---
Yesterday I realised that the last time I connected via RDP into a server was back in May.  
That talks volumes about how much cloud-native I am doing these days, but it also made me feel the burden of dealing with a Virtual Machine: logging in, dealing with the whole OS, an overall sense of slowness.

The reason why I logged in that VM is because I wanted to update one of my demo instances of SonarQube, which I use in all sorts of demos due to the amount of data I have in there.  

It's been a while since I updated that specific one, so it was about time. That is where my issues started - I tried to update to the latest LTS, no luck because of the version of Java I installed on the VM. The latest version of Java is not supported either, and retrieving specific versions of the JRE/JDK is not exactly straightforward. Then ElasticSearch complained, then something else.  

After a while I managed to get to the LTS, but then I had other errors when trying to move to the latest version. It's not SonarQube's fault in fairness, as much as mine as I neglected this specific demo instance. It was time to move away from a Virtual Machine and into something nimbler.

SonarSource now offers SonarQube via a [Docker image](https://hub.docker.com/_/sonarqube) - an amazing start. Running it with the H2 database is a breeze - either in a Web App or a container.  

I immediately excluded AKS due to my scenario not requiring the complexity of Kubernetes, so I started looking at Azure Container Instance. This is what you need if you only need to run a container in a lift-and-shift scenario, no need for any extra complexity.

SonarQube in ACI works a charm, but I wanted to use my own database - and that's where the problems begin. How do you pass the required information to SonarQube if you are running in ACI? And also - how do you keep control over the instance?

So, rolling up my sleeves - you can provision an ACI with [Environment Variables](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-environment-variables) which allow a user to inject variables into the target container at startup. SonarQube now [supports](https://docs.sonarqube.org/latest/setup/environment-variables/) them - so you need to setup your ACI with them:

![](/images/posts/2020-11-27_09-21-51.png)

If you provision this from scratch please use an ARM template like I did, it will allow you to set the SONARQUBE_JDBC_PASSWORD variable as a **secret string**!

So you can run SonarQube with a real database. But it won't start - you will get an error from [ElasticSearch](https://github.com/SonarSource/docker-sonarqube/issues/282). Long story short, you need real, persistent storage for ElasticSearch as you are now running a non-empty instance of SonarQube.

The easiest solution here is to create a Storage Account and to setup file shares to be passed to our ACI as [mount points](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-volume-azure-files). I did that for the four folders I was really interested in:

![](/images/posts/2020-11-27_09-28-59.png)

I wanted to keep control of the conf folder, the data folder, the extensions folder and the logs folder. Each one of them is mounted on the ```/opt/sonarqube/<folder>``` path - hence ```/opt/sonarqube/conf```, ```/opt/sonarqube/data```, etc.

For the conf folder, the reason why I wanted to keep it under my control was to upload a sonar.properties file containing properties I am interested in overriding by default (like the port to use, or the dreaded ```sonar.search.javaAdditionalOpts=-Dnode.store.allow_mmapfs=false```)

The data folder is necessary for ElasticSearch, the extensions folder is where you will find all the various installed plugins, and the logs folder contains all the SonarQube logs. This allows me to maintain a degree of control over the container in use, while still allowing the image to be refreshed anytime without worrying about breaking changes.

You can find my ARM template and deployment script [here](https://github.com/mattvsts/SonarQubeACI) - it is very simple, but it works for demo purposes. If you want to make it better, you should tighten the database firewall rules and add a nginx reverse proxy via the sidecar pattern so you can get HTTPS implemented too.