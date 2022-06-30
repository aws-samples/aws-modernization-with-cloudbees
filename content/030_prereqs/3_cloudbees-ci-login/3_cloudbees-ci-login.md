---
title: "CloudBees CI Login"
chapter: false
weight: 3
--- 

CloudBees CI for modern platforms takes advantage of Kubernetes by providing dynamic provisioning of team specific Jenkins instances we refer to as ***managed controllers***. In this lab you will login into a pre-provisioned CloudBees managed controller (Jenkins instance) with an initial configuration provided by CloudBees CI Configuration-as-Code.

## CloudBees CI Managed Controller

### Login to CloudBees CI

**Important**: this CloudBees CI controller is provided for this demo purpose only, do not use it for any other development beyond this workshop.

1. Login into the CloudBees CI Workshop cluster at: **https://cbci.aws.cb-demos.io/cjoc/**
2. Enter your username, which is the GitHub username you are using for this workshop, and the password `cb2022`, into the login screen and click the **Sign in** button. ![CloudBees CI Login](setup-login.png?width=40pc)
3. Click on the link of your CloudBees CI ***managed controller*** that will have the same name (lowercased) as your GitHub username with a `-controller` suffix and be in folder with the same name as the GitHub Organization you are using for this workshop. ![managed controller link](managed-controller-link.png?width=70pc) 
4. NOTE: Depending on when you completed the pre-workshop setup your ***managed controller*** may still be **Starting** as seen below. ![managed controller starting](starting.png?width=60pc) 
If that is the case you will have to wait until it is **Approved** and **Connected** as seen in the following screenshot. Once the **Status** is **Approved** and **Connected** click on the link for your managed controller. ![managed controller connnected](mc-connected.png?width=60pc) 

>NOTE: There are a number of ways to create a ***managed controller***. We take a very opinionated way to provision attendees ***managed controllers*** for this workshop in order to pre-configure the components that you will interact with during the workshop, allowing us to jump into the hands on content more quickly.
