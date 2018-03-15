---
layout: post
title: "Introduction to Circle CI"
date: 2017-10-24 20:06:55 +0530
comments: true
categories: [Ruby, Rails, CI]
---




## Intro && Setup Project

CircleCI helps you ship better code, faster. To kick things off, you'll need to add a config.yml file to your project, and start building. After that, we'll start a new build for you each time make a PR. Similar to travis; here also needed a yml file for configs and update.

## Steps

1.Signup using github

{% img /images/circleci/intro.png 800 300 %}

2. Add our Project

{% img /images/circleci/add_project.png 800 300 %}

3.
Create a folder named .circleci and add a fileconfig.yml (so that the filepath in .circleci/config.yml).

4.
Populate the config.yml with the contents of the below file.

<script src="https://gist.github.com/anoobbava/2c9417987a3e67210395119aa5083c48.js"></script>

5.
Update the config.yml to reflect your project's configuration.

6.
Push this change to GitHub.

7.
Start building! This will launch your project on Circle CI , now it will analyse the code and check the system for PR.all done, system will automatically test when make our PR.

{% img /images/circleci/circle_Pr.png 800 300 %}

Awesome, we got our error on build we can see what is the error.

{% img /images/circleci/circle_error_pr.png 800 300 %}

The issue is we have mentioned is ruby in gem file as 2.3.1 but in the config of circle is 2.4.1. we will update it as another commit.

I Found it, circle CI using docker images pre-built ones, Here we are using the ruby version 2.3.1 in Gemfile and the config.yml added 2.4.1. Going the below url 
[go to circle docs info](https://circleci.com/docs/2.0/circleci-images/#ruby)
- most matched version is 2.3; now we are commiting using that code. All work fine.Now we select the image,
We can select linux, IOS, or custom host in circle CI, For this tutorial I have used the linux plan, hobbyist one. We can use containers.

{% img /images/circleci/circle_all_test_passed.png 800 300 %}

{% if page.comments %}

{% endif %}