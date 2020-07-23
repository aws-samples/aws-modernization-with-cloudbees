+++

title = "Import Existing App"
chapter = true
weight = 40

+++

# Import Exsiting App

You will most likely have apps you’ve developed, so let’s go over how to import an app into Jenkins X and run it through CI/CD ultimately deploying it to the staging environment.

To import an app, you can execute the following CLI command, and specify the GitHub URL of your app.  For example, I am importing as follows:

```bash
jx import --url https://github.com/jenkins-oscar/carsweb.git
```
The CLI will ask what Git Username you would like to use to import the app, I select the personal GitHub account as shown below.  In my case, it is `sharepointoscar`

```bash
? Git user name: sharepointoscar
performing pack detection in folder /Users/omedina/git-repos/carsweb
--> Draft detected EJS (57.572451%)
--> Could not find a pack for EJS. Trying to find the next likely language match...
--> Draft detected JavaScript (26.858251%)
selected pack: /Users/omedina/.jx/draft/packs/github.com/jenkins-x-buildpacks/jenkins-x-kubernetes/packs/javascript
replacing placeholders in directory /Users/omedina/git-repos/carsweb
app name: carsweb, git server: github.com, org: jenkins-oscar, Docker registry org: jenkins-oscar
skipping directory "/Users/omedina/git-repos/carsweb/.git"
Let's ensure that we have an ECR repository for the Docker image jenkins-oscar/carsweb
Creating GitHub webhook for jenkins-oscar/carsweb for url https://hook-jx.jx.eks.sharepointoscar.com/hook
…….

Watch pipeline activity via:    jx get activity -f carsweb -w
Browse the pipeline log via:    jx get build logs jenkins-oscar/carsweb/master
You can list the pipelines via: jx get pipelines
When the pipeline is complete:  jx get applications

For more help on available commands see: https://jenkins-x.io/developing/browsing/

```

### What Just Happened?

There are several things that happened when we imported our application:

1. Jenkins X detected the language our app is written on and selected the appropriate Build Pack
2. Jenkins X added additional files to our repository which include a Helm Chart, skaffold.yaml amongst others
3. A new webhook was added to our app repository
4. A pipeline was automatically triggered to deploy the app to the Staging Environment, which also means a PR was created in the Staging GitHub repository
5. Lastly, the CLI outputs helpful commands to see the activity of the pipeline being triggered for this app.

**ChatOps** is at work here, and as you can see from the screenshot below, our bot account took care of merging the PR for the Staging environment, and the app was published.

![ChatOps](/images/chatops.png)


### List Deployed Apps

```bash
jx get applications

APPLICATION STAGING PODS URL
carsweb     0.0.1   1/1  http://carsweb-jx-staging.jx.eks.sharepointoscar.com

```

The app we just imported is now deployed in the staging environment. If you go to that URL you should see your application.  In my case this is what shows up (notice the staging URL)

![Staging App](/images/staging_app.png)