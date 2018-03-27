---
layout: post
title: "Automatically run the migrations in Heroku"
date: 2018-03-27 20:26:59 +0530
comments: true
categories:
---

We all know that Heroku Running on the PAAS(Platform As Service) architecture. It is free for starter applications or hobby projects. For a normal projects, deplolyment phase consists of below steps

1. select service
2. install OS
3. install Ruby
4. install Rails
5. Install dB
6. Install AppServer
7. configure All

trust me, it is not a simple task, I have tried it and it is always in pain when setup. Takes deep knowledge to master in deployment. But for heroku is so cool and no worries, But here we have not discussing that,we are facing and issue with migration and this migration need to run every time after the code is deployed.

We need to run the below code every time after "git push heroku master"

```
  reroku rake db:migrate
```

{% img /images/run-migration/1.png 800 300 %}

## Solution

thanks to Heroku, they created something called **release**, which will be like a after_update callback to call this process. for that need to add some code to the Procfile

### what is a Procfile

  As copied from heroku doc
  ```
  > A Procfile is a mechanism for declaring what commands are run by your application’s dynos on the Heroku platform. It follows the process model. You can use a Procfile to declare various process types, such as your web server, multiple types of workers, a singleton process like a clock, or the tasks you would like to run before a new release is deployed to production.
  > Every dyno in your application will belong to one of the process types, and will begin executing by running the command associated with that process type.

 create a file called **Procfile** in the Application root path, ensure no extensions and nothing more in the file

 Add the below code in to that file,

 ```
    release: rake db:migrate
 ```

hooray. all done, now do work, system will automatically check the migration files and executes them.

{% img /images/run-migration/2.png 1000 300 %}


### Note

this process explained on the assumption that, you know the deployment of heroku and enable automatic deployment using github also.

#### Automatic Deployment using Github

Heroku provides a service to deploy the code to production once we commited in a specific branch. For me, **release** is the deployment branch. Need to a simple step to do that

1. choose the **Deployment method** and connect to **Github**

{% img /images/run-migration/3.png 800 300 %}

2. in the **Automatic deploys** section select your branch,

{% img /images/run-migration/4.png 800 300 %}

I have configured the test suit by Travis CI, thats why checked the option **Wait for CI to pass before deploy**

all set. thanks guys, comment if any error or doubt happend
