---
layout: post
title: "GCP:4 deployment using mina"
date: 2018-06-28 21:18:28 +0530
comments: true
categories: [ruby, GCP, Rails, mina]
---
## Introduction

This is the last blog which deals with the GCP deployment, here our main area of
topic is the mina "a blazing fast deployment tool".Which is executed as a
Rake.Also need to install and setup is pretty, no worries. Advantage is that we
check-in the code to the github.Only the place is the config/deploy.rb.Also we
can implement DRY principle to the deployment script.Which means;we can use the
same script to deploy the app to staging, QA and even Production.

{% img /images/mina/1.png 400 100 %}

[mina github link](https://github.com/mina-deploy/mina)

##How the deployment process done ??

 We are dividing the deployment to below section to easily understand and
deployment.

 1. setup and install mina gem
 2. mina Rake
 3. script to deploy
 4. running the Rake.
 5. setup nginx and unicorn
 6. known issues while occured in the deployment and fixing.

### 1.Setup and install mina gem

{%img /images/mina/2.png 600 100 %}

Add the below gem to the development group.

```
  gem 'mina', '~> 1.2', '>= 1.2.3'
```
Now what we need to add is the mina-unicorn gem, this will used to deploy
unicorn with mina.

```
  gem 'mina-unicorn', '~> 2.0'
```
then do

```
  bundle install
```
### 2.mina Rake

mina works like a rake task.There is a another command

```
  mina init
```
it will create the configuration file in the config/deploy.rb

{% img /images/mina/3.png 400 100 %}

Hooray, A major part is done, now we need to add the tasks we are going to use
in the *deploy.rb*
You can use your own tasks, based on the taste, but i would like to follow the
old practices like the setup and deploy

*setup*

In this rake, we are going to deals with the basic details like creating the
folders, creating the temp folders, etc.

*deploy*

This rake mainly deals with clone the app and kill the pid, bundle install, migrate the app, migrate, precompile the assets.

###3.mina script

deploy.rb is the heart of the mina tool.We can configure that based on our requirement.I will give you basic explanation about the each of the commands here and updated the basic skeleton of the deploy.rb and also for verification, will updated with my own deploy.rb which is used in my blog_app.

*skeleton of the deploy.rb*

<script src="https://gist.github.com/anoobbava/905c8aa332078d9ee4128e6b312484b1.js"></script>

*copy of my original deploy.rb file*

<script src="https://gist.github.com/anoobbava/2240c4066d39db1cebe3b787ad37e630.js"></script>

Now our scripts are done.Copy this file into your app/config/deploy.rb file and

run the commands below,

### 4.Running the Rake

Before running the rake, ensure that you are added the* mina gem and mina-unicorn*
and bundle installed.

first run the command

```
  mina setup
```
{% img /images/mina/4.png 600 200 %}

Now the setup execution is completion is success, there is nothing to worry in
this, now we are moving to the deploy command.


```
  mina deploy
```
{% img /images/mina/5.png 900 400 %}

{% img /images/mina/6.png 900 400 %}

{% img /images/mina/7.png 900 400 %}


ah!!, We got the first error, that issue is because we don't specify the database
and the connector, then user name and password in the path.In order to do that,
go to our server terminal

{% img /images/mina/8.png 800 400 %}

Now we go to the app path , here it is blog_app/

{% img /images/mina/9.png 600 100 %}

Now go to the blog_app/ folder go to the *shared/config/* there is a file called
the database.yml and add the connection details there.

```
staging:
  adapter: postgresql
  encoding: unicode
  database: blog_app_staging
  pool: 5
  host: localhost
  username: blog_user
  password: password
```
{% img /images/mina/10.png 600 100 %}

ah!, we got another error, that error comes because there is no database
configured.It is possible to create the database from the mina tool;but we will
do via console and we will explain that in another blog.

{% img /images/mina/11.png 900 400 %}

Now, we will create a database by logging to the server and using the below
command

```
  sudo -i -u postgres
```
then using the below command, generate the database

```
  createdb databasename
```
{% img /images/mina/12.png 600 100 %}

Next is grant access to the user to the new database.

```
  grant all privileges on database databasename to username;
```

{%img /images/mina/13.png 900 400 %}

Please check the above image before executing the above command.

Now again will do the *mina deploy*

{% img/images/mina/14.png 900 400  %}

Awesome, we are good to go, our app is deployed,but it is not for accessing our
browser, need to do some tweaks, Great working guys.

###5.setup nginx and unicorn

Now, I want to check whether the nginx can be accessible via ip-address.

just go to ip-address in the browser,

{%img /images/mina/15.png 600 300 %}

Awesome, you got the output, now only some tweak is needed.

first update the nginx configuration with below configuration, it is normal
config, only we need to know about the pid file and error logs.

<script src="https://gist.github.com/anoobbava/5d8bb925578412b3b3f1e500a68010e5.js"></script>

now copy the config to the */etc/nginx/sites-enabled/default* file.

then restart the nginx using the

```
  sudo service nginx restart
```

{%img /images/mina/16.png 900 400 %}

now nginx is okay, please check the browser we are hitting and also check the
log if any errors are happening.Log will be in the below path

*/var/log/nginx/error.log* and */var/log/nginx/access.log*

Awesome!!, it is hitting the nginx, but  the page is not loaded, so the issue is
with the unicorn, we will check the unicorn logs for this.

unicorn log will be in the *blog_app/shared/log/unicorn.stderr.log*

{% img /images/mina/17.png 900 400  %}

tailing this error will reveal the real issue (ie tail -f nicorn.stderr.log)

{% img /images/mina/18.png 900 400 %}

cool, the error is because, we have not set the secret key base, in the
secrets.yml, need to set that and then proceed.

{%img /images/mina/19.png 900 400 %}

by running the below command from the current path in the server console,

```
  bundle exec rake secret
```

then update the command in the *config/shared/secrets.yml* with like below

{% img /images/mina/20.png 900 400 %}

{%img /images/mina/21.png 900 400 %}

{%img /images/mina/22.png 900 400 %}

the reason for staging, we are deployed to staging server.

Now, repeat the steps like we already done

1. restart the nginx

2. check the status of the nginx

3. mina deploy from the project terminal(not from the GCP terminal!!!)

3. tail -f /var/log/nginx/access.log to check it is hitting or not!!!

4. go to the ip-adress in the browser,

{%img /images/mina/23.png 900 400 %}

hooray, we are all done, now we need to explore additional options like,how to
store the images, login issues etc. Please comment me if any issues happend
