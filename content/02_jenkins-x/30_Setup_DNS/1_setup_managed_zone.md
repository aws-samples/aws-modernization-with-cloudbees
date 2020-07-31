+++

title = "Create Route 53 Managed Zone"
chapter = false
weight = 1

+++


Part of our scenario is to configure Jenkins X with a custom domain.  To do this, we must first configure a Route 53 Managed Zone then delegate your subdomain to Route 53.  My domain is hosted elsewhere with an NS record delegated to route53.


## Create a Managed Zone for subdomain

1. Create a Managed Zone in Route 53 for your subdomain.
2. Delegate your subdomain to AWS Route 53 from the vendor hosting your domain by creating an **NS** record and   pasting the  NS Server entries Route 53 provided when you created the Managed Zone.
3. Test DNS it using `dig` or the Route 53 console.

{{% notice warning %}}
When testing the Hosted Zone can be done from the AWS Console, your goal is to get response with **NOERROR** as shown below.  You cannot move forward without DNS working properly.
{{% /notice %}}


The following image shows the configuration and DNS response.

![''](/images/route53.png)

