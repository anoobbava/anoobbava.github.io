---
layout: post
title: "Continous Integration using Travis CI"
date: 2017-10-17 23:57:58 +0530
comments: true
categories: [Ruby, Rails, CI, Travis]
---

## Why Travis CI

Before you start in to our CI, one must understand what is CI and why the CI is going to help us the development and what is a *DevOps*.

![Image of Travis CI](images/travis_logo.png)

## DevOps
* Is a combination of cultural philosophies.
* combined to do deviler the products at High Speed.
* development and operations teams are no longer "siloed."(AWS)
* Technology is in path we can minimise the effort and reduce the bugs from the existing system.
* DevOps help us to achive better results in minimal Time.
* when Continous Integration and Continous Delivery makes us to reduce the development time.

![devops](images/travis_devops.jpeg)

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
![work flow](images/travis_work_flow.png)
### PR work flow
![PR flow](images/travis_pr_workflow.png) 

## prerequisites
* Active Github Account.
* Need to link to Github repo with Travis CI.
* test coverage for system.

Here we are testing for Ruby on rails.To test our project has test coverage we are using the simplecov gem.Testing using SimpleCov is explained in this [link](https://anoobbava.wordpress.com/2017/10/03/find-test-coverage-locally/)
![simple cov](images/travis_simple_cov.png)
## Back in Action
Next thing what we do is to Login with Github
![github login](images/travis_sigin-with-gituhb.png)

All the gitHub Repo's are synched to the Travis-CI.Now Turn ON the Switch against the Repos. We need to update a YML file for travis to automate the testing.There is an online tool to validate the Travis YML using this [link](https://lint.travis-ci.org/).Right now we are discussing only the simple ones for start.

## Sample YML
In order to function the Travis and install the depandancies, need a config file. travis.yml is that kind of file will help us to implement that feature. Below is sample file. There are other numerous configs, here is the basic to start and running.
<script src="https://gist.github.com/anoobbava/712777537f3d2653db2819b5add3402c.js"></script>

Mentioned only the Ruby and the Version. Also before starting our testing, we need to setup a test database.The reason is we don't want to test the production dB by any chance. Now comes the script part, we are migrating the database to the latest structure and running the rspecs. Addons are something we can add the result of the test details to another tool like codeclimate. I have used the codeclimate, will report the test coverage to gitHub also. Next is commit this code and push to master. We can config the travis to run only at the time of PR(Settings of Travis CI corresponding project).
Need to check the settings of the travis-ci of particular repo, like when the build started or start build only when the yml is present like that.
![Travis config](images/travis_settings.png)

#### Now it is check-in time.Add the code and made a PR

![checkin the code](images/travis_checkin.png)

#### After made PR, the Travis-CI is analysing the code

![travis pr checking](images/travis_pr_checking.png)
#### we can see the status of PR by clicking on the see details from gitHub page.

![travis success](images/travis_success.png)
#### Hooray, all success, now we can see the detailed log for details.

![travis log](images/travis_log.png)

Image courtesy: [travis](https://www.travis-ci.org/)

{% if page.comments %}

{% endif %}