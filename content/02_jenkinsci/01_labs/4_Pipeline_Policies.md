+++
title = "Pipeline Policies"
chapter = true
weight = 50
+++

# CloudBees CI - Pipeline Policies

## Create a Pipeline Policy

In this lab you will create a [Pipeline Policy](https://docs.cloudbees.com/docs/admin-resources/latest/pipelines-user-guide/pipeline-policies) to ensure that all Pipeline jobs that run on your Team Master have a 30 minute global `timeout` set.

[Instructor led video of lab.](https://youtu.be/4J8S-9Ux-GI)

1. Navigate to the top-level of your Team Master and click on **Pipeline Policies** in the left menu. <p><img src="../../images/policies-click.png" width=800/>
2. Click on **New Policy**<p><img src="../../images/new-policy-click.png" width=600/>
3. Fill out the Pipeline Policy parameters:
   1. **Name**: Timeout policy
   2. **Action**: Fail
   3. Click on **Add Rule** button: 
      1. Select **Pipeline Timeout**
      2. **Timeout**: 30 MINUTES
   4. Click the **Save** button <p><img src="../../images/policy-timeout-form.png" width=800/>
4. Navigate back to the **master** branch job for the **microblog-frontend** Mutlibranch project and click the **Build Now** link in the left menu. <p><img src="../../images/build-with-policy.png" width=800/>
5. Navigate to the logs for that build and you will see that the build failed due to **Validation Errors** <p><img src="../../images/pipeline-policy-error.png" width=800/>
6. To fix this we will have to update the `Jenkinsfile` of the **VueJS** template in your forked copy of the **pipeline-template-catalog** repository - remember, even though we are building the code in the **microblog-frontend** repository the `Jenkinsfile` is actually coming from the **VueJS** template. Navigate to that `Jenkinsfile` and the click the **pencil icon** to open it in the GitHub editor. <p><img src="../../images/pipeline-policy-open-jenkinsfile.png" width=800/>
7. In the GitHub editor, uncomment the `timeout` pipeline `option` and then click the **Commit changes** button to commit the updated `Jenkinsfile` to your **master** branch. <p><img src="../../images/pipeline-policy-fix-commit-jenkinsfile.png" width=800/>
8. Next, to ensure that we are using the updated **VueJS** template, we will **re-import** the Pipeline Template Catalog you just updated. Navigate to the top-level of your Team Master and click on **Pipeline Template Catalogs** in the left menu and then click the **workshopCatalog** link. <p><img src="../../images/workshop-catalog-link.png" width=800/>
9. On the next screen, click the **Run Catalog Import Now** link.  <p><img src="../../images/click-import-link.png" width=800/>
10. After the import is complete, navigate back to the **master** branch job for the **microblog-frontend** Mutlibranch project and click the **Build Now** link in the left menu. The build will complete successfully and the logs for that build will show that the Pipeline policy validated successfully. <p><img src="../../images/pipeline-policy-success.png" width=600/>

**For instructor led workshops please return to the [workshop slides](https://cloudbees-ci-aws-workshop.github.io/core-rollout-flow-workshop/core/#37).**

You may proceed to the next lab: [*Cross Team Collaboration*](../01_labs/5_cross_team_collab.html) or choose another lab on the [Main Lab Page](../01_labs.html).