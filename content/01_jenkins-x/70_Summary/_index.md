+++

title = "Summary"
chapter = true
weight = 60

+++

# Summary

In this worhsop we walked through creating an EKS cluster, then installing Jenkins X via its new Jenkins X Boot declarative way.  We then imported an existing application from GitHub, which immediately triggered a pipeline to deploy it to the staging environment.

Along the way, we saw how ChatOps is used, as the bot account intercepts and acts accordingly via the PR comments, ultimately merging PRs and triggering deployment pipelines.

We also got a glimpse of GitOps in action, as we saw the app deployed to its respective environment, it was via a Pull Request that all was being tracked.  Yes, Git was the source of truth all along.  We then promoted the app to production.


Learn more about Jenkins X at [Jenkins X](http://jenkins-x.io)