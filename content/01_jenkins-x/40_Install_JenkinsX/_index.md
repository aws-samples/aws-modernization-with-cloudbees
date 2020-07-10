+++

title = "Install Jenkins X on EKS"
chapter = true
weight = 30

+++

# Install Jenkins X on EKS

We will be using a stable distribution of the open-source Jenkins X project, otherwise known as CJXD (CloudBees Jenkins X Distribution).  The advantage of using this edition vs. the straight OSS is that it has been tested, and certified for EKS, it also allows for a controlled platform upgrade within your enterprise environment.

At this point, we have a clean cluster named **drymartini**, which is using Kubernetes 1.14 as shown below.

{{% notice note %}} As of the writing of this workshop, **Kubernetes 1.14** is what I am using.  However, Jenkins X should support 1.16 once it is available on AWS EKS. 
{{% /notice %}}


