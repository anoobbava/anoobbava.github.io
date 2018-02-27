---
layout: post
title: "Continous Integration using Travis CI"
date: 2017-10-17 23:57:58 +0530
comments: true
categories: [Ruby, Rails, CI, Travis]
---

## Why Travis CI

Before you start in to our CI, one must understand what is CI and why the CI is going to help us the development and what is a *DevOps*.

<!-- ![Image of Travis CI](images/travis_logo.png) -->
{% img /images/travis_logo.png 600 300 %}

## DevOps
* Is a combination of cultural philosophies.
* combined to do deviler the products at High Speed.
* development and operations teams are no longer "siloed."(AWS)
* Technology is in path we can minimise the effort and reduce the bugs from the existing system.
* DevOps help us to achive better results in minimal Time.
* when Continous Integration and Continous Delivery makes us to reduce the development time.

<!-- ![devops](images/travis_devops.jpeg) -->
{% img /images/travis_devops.jpeg 500 300 %}

## CI(Continous Integration)
* Is a development practice.
* requires developers to share the code to a common repository.
* Each code update is tested by automated build.
* if only the automated build is succeeded, then the code is updated to the system.
* we have Travis CI, Circle CI for this task.

## Travis CI intro
* Simple and powerful tool for the CI.
* Always free for the Open source repository.
* Test and deploy with Confidence.(motto)
*  [go to Travis](https://www.travis-ci.org/)
* facebook and Rails are using this.

### workflow
<!-- ![work flow](images/travis_work_flow.png) -->
{% img /images/travis_work_flow.png 1000 800 %}

### PR work flow
<!-- ![PR flow](images/travis_pr_workflow.png)  -->
{% img /images/travis_pr_workflow.png 1000 800 %}

## prerequisites
* Active Github Account.
* Need to link to Github repo with Travis CI.
* test coverage for system.

Here we are testing for Ruby on rails.To test our project has test coverage we are using the simplecov gem.Testing using SimpleCov is explained in this [link](https://anoobbava.wordpress.com/2017/10/03/find-test-coverage-locally/)
<!-- ![simple cov](images/travis_simple_cov.png) -->
{% img /images/travis_simple_cov.png 1000 800 %}
## Back in Action
Next thing what we do is to Login with Github
<!-- ![github login](images/travis_sigin-with-gituhb.png) -->
{% img /images/travis_sigin-with-gituhb.png 500 200 %}

All the gitHub Repo's are synched to the Travis-CI.Now Turn ON the Switch against the Repos. We need to update a YML file for travis to automate the testing.There is an online tool to validate the Travis YML using this [link](https://lint.travis-ci.org/).Right now we are discussing only the simple ones for start.

## Sample YML
In order to function the Travis and install the depandancies, need a config file. travis.yml is that kind of file will help us to implement that feature. Below is sample file. There are other numerous configs, here is the basic to start and running.
<script src="https://gist.github.com/anoobbava/712777537f3d2653db2819b5add3402c.js"></script>

Mentioned only the Ruby and the Version. Also before starting our testing, we need to setup a test database.The reason is we don't want to test the production dB by any chance. Now comes the script part, we are migrating the database to the latest structure and running the rspecs.I have used the codeclimate.

## Why Codeclimate

codeclimate is a code analysis engine will help to check the code has any issues using gems like breakman and rubocop.Also it has built in analysis engine will help us to analyse the code test coverage and also numerous features like badge for our GitHub account. signup using your Github and authorise access codeclimate to our repo. An advantage is that for opensource repo; the codeclimate is free for lifetime, Cool and Awesome right, thanks to codeclimate for their services. 
Login to codeclimate account and goto our repo, settings tab> Test Coverage. there is a token is present. This token is a link between Travis CI and codeclimate.
{% img /images/travis_test_coverage_cc.png 1000 800 %}
Now see the magic, login to our travis account, goto our project> more options > settings > Environment Variables 
{% img /images/travis_environment.png 1000 800 %}

create a new environment variable CODECLIMATE_REPO_TOKEN and copy the value from the codeclimate account.

All Set, now only simple task is copy the same token to the .travis.yml file also where XX marked.

note : I am taking the images from my another project for clarity, do not need to confuse with that :D

<script src="https://gist.github.com/anoobbava/79bfabda8e9ef4fdf35f75161920d0ae.js"></script>

Dont forget to add this gems our test group.


checkout the below the code if any doubts with the spec_helper.
<script src="https://gist.github.com/anoobbava/e197d468b7f8d8cc3e404fed9ced1b38.js"></script>

. Next is commit this code and push to master. We can config the travis to run only at the time of PR(Settings of Travis CI corresponding project).
Need to check the settings of the travis-ci of particular repo, like when the build started or start build only when the yml is present like that.
<!-- ![Travis config](images/travis_settings.png) -->
{% img /images/travis_settings.png 800 200 %}
#### Now it is check-in time.Add the code and made a PR

<!-- ![checkin the code](images/travis_checkin.png) -->
{% img /images/travis_checkin.png 600 200 %}

#### After made PR, the Travis-CI is analysing the code

<!-- ![travis pr checking](images/travis_pr_checking.png) -->
{% img /images/travis_checkin.png 600 200 %}
#### we can see the status of PR by clicking on the see details from gitHub page.

<!-- ![travis success](images/travis_success.png) -->
{% img /images/travis_success.png 600 200 %}
#### Hooray, all success, now we can see the detailed log for details.

<!-- ![travis log](images/travis_log.png) -->
{% img /images/travis_log.png 800 300 %}

Image courtesy: [travis](https://www.travis-ci.org/)

{% if page.comments %}

{% endif %}