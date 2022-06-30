---
title: "Hibernation for Managed Controllers"
chapter: false
weight: 6
---

The [CloudBees CI hibernation for Managed Controllers](https://docs.cloudbees.com/docs/cloudbees-core/latest/cloud-admin-guide/managing-masters#_hibernation_in_managed_masters) feature takes advantage of running CloudBees CI on Kubernetes by automatically [scaling the Kubernetes replicas](https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/#scaling-a-statefulset) of a CloudBees CI Managed Controller [Statefulset](https://kubernetes.io/docs/tutorials/stateful-application/basic-stateful-set/) to zero (think of it as shutting down) after a specified amount of inactivity. This results in no Kubernetes pods running for the CloudBees CI Managed Controller Stateful set and no cpu or memory cluster resources being used. This feature will also automatically scale up the replicas of a CloudBees CI Managed Controller Statefulset to one (think of it as starting up a controller) for certain events such as GitHub webhooks, Jenkins cron based job triggers and any HTTP GET to the [GET proxy for hibernation](https://docs.cloudbees.com/docs/cloudbees-ci/latest/cloud-admin-guide/managing-masters#_get_proxy_for_hibernation) link for a Managed Controller. And because a Kubernetes Statefulset is being used to run the Managed Controller on Kubernetes, the persistent state (i.e. Jenkins home) of the controller is preserved between these shut down (replicas scaled to zero) and start up (replicas scaled to one) actions - meaning your CloudBees CI Managed Controller will be in the exact same state as it was when it shut down.

## Hibernation Proxy for Webhooks

The hibernating monitor service provides a `POST` proxy for things like GitHub webhooks. In this lab we will update the GitHub webhook of your workshop GitHub Organization to use the [CloudBees CI hibernation POST queue endpoint](https://docs.cloudbees.com/docs/cloudbees-ci/latest/cloud-admin-guide/managing-masters#post-queue-github) instead of the GitHub webhook posting directly to your Managed Controller. 

Hibernation for CloudBees CI Managed Controllers is managed at the global Jenkins configuration level and for this workshop it has been configured by the `jenkins.yaml` file of your CloudBees CI configuration bundle. We will need to override that value, temporarily, to get through this lab more quickly.

1. First, we will update the hibernation grace period of your managed controller so we don't have to wait 25 minutes for it to hibernate (gracefully shut down). To modify the hibernation configuration via the UI you will need to login as an administrator. Click on your CloudBees CI username in the top-right corner of the screen and then select **Log Out** from the drop-down menu. ![Log Out](log-out.png?width=50pc)
2. Log back in, but append **`-admin`** to the GitHub username you used earlier to login with, the password is the same as before. ![Log In as Admin](log-in-admin.png?width=50pc) 
3. Navigate to the top-level of your managed controller, click on the **Mange Jenkins** link in the left menu and then click **Configure System**. ![Manage Jenkins](manage-jenkins.png?width=50pc)
4. Scroll down to the **Automatic hibernation** configuration and update the **Grace period** from *1500* seconds (configured via CasC) to *10* seconds and then click the **Save** button. ![Update Grace period](update-grace-period.png?width=50pc)
5. Next, navigate to the top level CloudBees CI Cloud Operations Center and refresh the page until your managed controller is hibernating signified by a *blue pause icon*. ![Hibernating Managed Controller](hibernating-controller.png?width=50pc)
6. Click on the **Manage** link, signified by the *cog icon*, for your managed controller and on the **Manage** screen for your controller you will see that your managed controller is **Disconnected (hibernated)** and also note that the **Statefulset** for your managed controller has 0 replicas - that is no pods using any cluster resources. ![Disconnected Hibernated Controller](disconnected-hibernated-controller.png?width=50pc)
7. Now goto to your workshop GitHub Organization and click on the **Settings** link. ![GitHub Organization Settings link](github-org-settings-link.png?width=50pc)
8. In the **Account settings** left menu click on the **Webhooks** link and then click on the **Edit** button for the Webhook starting with **https://cbci.workshop.cb-sa.io/**. ![Edit CBCI Webhook](edit-webhook-button.png?width=50pc)
9. Before we update the webhook to use the hibernation proxy, scroll down to **Recent Deliveries**, expand the most recent delivery and click the **Redeliver** button. The *redelivery* will fail with a *503 Service Temporarily Unavailable* response. ![Failed Webhook Redelivery](failed-webhook-redelivery.png?width=50pc)
10. Now we will update the **Payload URL** to send Webhooks to the `hibernation/queue/` - in this example we are setting it for a GitHub Organization with the name **bee-ci** so the payload URL will become `https://cbci.workshop.cb-sa.io/hibernation/ns/controllers/queue/bee-ci-controller/github-webhook/` - update your **Payload URL** by replacing `https://cbci.workshop.cb-sa.io/` with `https://cbci.workshop.cb-sa.io/hibernation/ns/controllers/queue/` before your managed controller specific sub-path and then click the **Update webhook** button. ![Update webhook](update-webhook-url.png?width=50pc)
11. Once again, scroll down to **Recent Deliveries**, expand the most recent delivery (the one that failed) and click the **Redeliver** button. The redelivery should succeed. 
12. Navigate to the **Manage** screen for your managed controller and refresh your browser. **IMPORTANT - DO NOT CLICK ON THE LINK FOR YOU MANAGED CONTROLLER!** Although you should still see that your managed controller is **Disconnected** you should also see that the **Statefulset** has **1/1 replicas**. ![Managed Controller unhibernating](controller-unhibernating.png?width=50pc)
13.  After a few minutes your managed controller will no longer be hibernated. ![Managed Controller Running](controller-running.png?width=50pc)

{{% notice note %}}
If you review the **Automatic hibernation** configuration for your Managed Controller after it is running again, you will see that the hibernation **Grace period** has been reconfigured to a value of ***1500*** second (25 minutes) based on the value configured in the CloudBees CI configuration bundle for your managed controller as the configuration bundle values will always override any UI based changes.
{{% /notice %}}

## Un-hibernate a Managed Controllers via the Operations Center UI

These instructions are intended to be used when returning to use your CloudBees CI Workshop managed controller after it has been idle for 25 minutes or more.

1. Navigate to the top level of Operations Center and find your CloudBees CI managed controller (Jenkins instance) in the list of CloudBees CI Managed Controllers - typically the only one listed. 
2. If there is a light blue **pause** icon next to your CloudBees CI managed controller then it is hibernating and if there is not a light blue **pause** icon next to your CloudBees CI managed controller then refresh your browser until there is one. Just click on the link for your Managed Controller to have its Kubernetes Statefulset replicas scaled up from zero to one. ![Hibernating managed controllers](hibernating-controller.png?width=50pc)
3. Once you click on your CloudBees CI managed controller link from the classic UI of Operations Center you will see a screen that shows that it is "getting ready to work". ![Un-hibernate](unhibernate.png?width=50pc)
4. After a couple of minutes, your CloudBees CI managed controller will be ready to use and in the same state as it was when it was hibernated.
