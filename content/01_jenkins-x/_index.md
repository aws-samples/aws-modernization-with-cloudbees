---
title: "Module 1"
chapter: true
weight: 2
---

# Continuous Delivery with EKS and Jenkins X

![EKS and Jenkins X](images/banner.png)

## Welcome

In this workshop you will learn how to quickly get up and running using EKS and Jenkins X. We'll explore how to create a fully operational continuous delivery pipeline using Docker containers, EKS, Jenkins X, and quite a few other tools to establish your Kubernetes-native CI/CD process.

All with the goal of having your developers focus on delivering features fast!

## What You Will Learn
At the end of this workshop, you will have learned how to get up and running with EKS and Jenkins X, run your apps through CI/CD in Jenkins X and publish them to a staging environment.



  <div style="font-size:22px"><i class="fas fa-check-square fa-fw" style="color:Green;valign=middle"></i> Installing Jenkins X on newly created EKS cluster using Jenkins X Boot</div>
 
   <div style="font-size:22px"><i class="fas fa-check-square fa-fw" style="color:Green;valign=middle"></i> Configure a custom domain FQDN: jx.eks.sharepointoscar.com and TLS</div>

   <div style="font-size:22px"><i class="fas fa-check-square fa-fw" style="color:Green;valign=middle"></i> Importing an existing app from GitHub and running it through CI/CD</div>

   <div style="font-size:22px"><i class="fas fa-check-square fa-fw" style="color:Green;valign=middle"></i> Explore ChatOps in the context of Jenkins X</div>

   <div style="font-size:22px"><i class="fas fa-check-square fa-fw" style="color:Green;valign=middle"></i> Explore GitOps and how it works with Jenkins X environments</div>




{{% notice information %}}
<p style='text-align: left;'>
You can create your EKS cluster using any method you’d like, such as using the eksctl CLI tool or Terraform.  From the Jenkins X perspective,  how you create your cluster does not matter.  We used eksctl to create the cluster we are working with today. 
</p>
{{% /notice %}}

## Solution Diagram
![solution design](images/eks_jenkins-x.png)