+++

title = "Promote App to Production"
chapter = true
weight = 50

+++

# Promoting the App to Production

At one point when the application is ready, you’ll want to push it to production.  To do that, you will want to execute the following command.

```bash
jx promote --app carsweb --version 0.0.1 --env production
```

This effectively will publish the app to the production environment by creating a PR in the production Github repository.  

In this example app, the staging environment shows a special UI message in yellow as shown earlier.  For the production environment, this should not show up.

![Production App](/images/production_app.png)

As you can see from the URL our production environment now has the same version of our app running in production as well.