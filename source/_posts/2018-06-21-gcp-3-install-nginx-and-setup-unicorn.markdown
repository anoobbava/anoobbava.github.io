---
layout: post
title: "GCP:3 Install Nginx and Setup Unicorn"
date: 2018-06-21 18:15:15 +0530
comments: true
categories: [ruby, Rails, GCP, nginx, unicorn]
---
## Introduction
Hi All, this is the 3rd post of our deployment tool, so far we have covered the Setup for instance and installing ruby and postgres. Now what we want is to install the Nginx and Unicorn. Nginx is our App server and Unicorn is our web server. We are Not going to explain about the concepts of nginx and Unicorn; instead we used these tools to deploy our App.We already had a staging server, we used that to setup and installation.

### A little House keeping

Image of the staging server is running.

{% img /images/gcp3/1.png 600 400 %}

terminal connection in staging server

{% img /images/gcp3/2.png 600 400 %} 

### Setup Nginx

```
  sudo apt-get install nginx
```
{% img /images/gcp3/3.png 600 100 %}

Now Check the nginx status using

```
  sudo service nginx status
```
{% img /images/gcp3/4.png 600 100 %} 

other commands

to restart nginx

```
sudo service nginx restart
```

to stop the nginx

```
  sudo service nginx stop
```
to start the nginx

```
  sudo service nginx start
```
here we are not configuring the nginx right now, we will do that later.

### Installing Unicorn

 Like I already said, we are using the unicorn as app server,by default puma is
the development server with Rails 5.X.X.

1.add the unicorn gem to production group
```
  gem 'unicorn'
```
{% img /images/gcp3/5.png 400 100 %} 

2. add the unicorn configuration file in config/ path

{% img /images/gcp3/6.png 800 100 %} 

Consider only the unicorn.rb file only.The total scripts are added below for
verification, Like I already said, there are a lot of configurations are there.
Just google it for details.

<script src="https://gist.github.com/anoobbava/cb5b1fa5a71f73a204a6c51ea1e03c08.js"></script>

3.commit these code changes to our code base, since I have already commit those,
 I don't want do it again.
I know, it is only a short blog, we just covered here, will explained about
deployment using mina in the next blog,!!promise

