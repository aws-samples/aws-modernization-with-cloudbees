---
title: "Using Pipeline Templates"
chapter: false
weight: 2
---

## Create a Job from Pipeline Template Catalog
In this lab you will create a new Multibranch Pipeline job from the **Maven Pipeline Template** provided by a Pipeline Template Catalog. And just by filling in a few parameters of a Pipeline template, you will quickly have a complete continuous integration pipeline for your application that meets the required standards of your organization.

1. On your CloudBees CI Managed Controller (Jenkins instance) navigate into the **template-jobs** folder.
2. Click on the **New Item** link in the left navigation menu.
3. Enter ***simple-maven-app*** as the Item Name, select **Maven Pipeline Template** as the item type and then click the **OK** button. ![New Maven Job](create-maven-job.png?width=60pc)
4. On the next screen, fill in the **GitHub Organization** template parameter with the name of the GitHub Organization you created for this workshop (all the other default values should be correct) and then click the **Save** button. ![Maven template Parameters](maven-template-params.png?width=50pc)
5. After you click the **Save** button the Multibranch Pipeline project (created by the template) will scan your `simple-java-maven-app` repository, creating a Pipeline job for each branch where there is a marker file that matches `cloudbees-ci.yml` (or in this case, just the `main` branch). Click on the **Scan Repository Log** link in the left menu to see the results of the branch indexing scan. ![Scan Log](maven-template-scan-log.png?width=50pc) 
6. Next, click on the **simple-maven-app** link in the menu at the top of page and you will see that there were no jobs created under the **Branches** or the **Pull Requests**. The reason is because the **Maven Pipeline Template** requires a **marker file** in each branch of the target repository that you want to be built by the template. ![No jobs](no-jobs.png?width=50pc) 
   - As you can see in the excerpt below, the **Maven Pipeline Template** specifies a `markerFile` (for details see [Using a custom marker file with templates](https://docs.cloudbees.com/docs/admin-resources/latest/pipeline-templates-user-guide/managing-multibranch-pipeline-options#_using_a_custom_marker_file_with_templates)) with a value of `cloudbees-ci.yml` in its `template.yaml` configuration (excerpt below taken from the `templates/maven/template.yaml` file you can find in your copy of the `pipeline-template-catalog` repository in your workshop GitHub Organization): 
   ```
   version: 1
   type: pipeline-template
   name: Maven Pipeline Template
   templateType: MULTIBRANCH
   description: Provides a pipeline template for maven builds.
   parameters:
   ...
   multibranch:
     markerFile: cloudbees-ci.yml 
     branchSource:
       github:
       ...
   ```
7. Now, in **GitHub**, navigate to your `simple-java-maven-app` repository in the GitHub Organization you created for this workshop, click on the `example.cloudbees-ci.yml` file, then click **pencil** icon to edit the file and then rename the file by deleting `example.` from the beginning of the file name, leaving just `cloudbees-ci.yml`. ![Rename Marker File](rename-marker-file.png?width=50pc)
8. Scroll to the bottom of the page and click the **Commit changes** *(directly to the `main` branch)* button to commit the renamed `cloudbees-ci.yml` to the **main** branch of your `simple-java-maven-app` repository. 
9.  Navigate back to the **simple-maven-app** Multibranch Pipeline on your CloudBees CI Managed Controller and you will see that there is now a **main** branch job. 

{{% notice note %}}
The job will fail and that is expected. We will fix the error in a subsequent lab.
{{% /notice %}}
![Maven main job](maven-main-job.png?width=50pc)
