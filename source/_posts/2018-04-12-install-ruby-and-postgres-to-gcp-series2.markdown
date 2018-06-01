---
layout: post
title: "install ruby and postgres to GCP:Series2"
date: 2018-04-12 15:51:22 +0530
comments: true
categories: [gcloud, Ruby, Rails, Deployment]
---

Hi All, Welcome to series 2, here are explaining about the ruby and Postgres installation to our GCP Server. If you know about that in linux 16.04 version, you can skip this tutorial. this is entirely based on the ubuntu 16.04 LTS machine and not much . I read the digital ocean, GoRails etc to publish this article and use the tehniques explained by them also.

## Install Ruby

  first need to connect to our GCP using pem file.

  {% img /images/series2/0.png 800 400 %}

### Install RVM

#### connect gpg keys

```
    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```

  {% img /images/series2/2.png 800 400 %}

#### Install curl

  install curl if not installed

  {%codeblock%}
    sudo apt-get install curl
  {%endcodeblock%}

  {% img /images/series2/3.png 800 400 %}
#### Use curl for rvm script

  Now use the curl to install the rvm script

  {%codeblock%}
    \curl -sSL https://get.rvm.io -o rvm.sh
  {%endcodeblock%}

  {% img /images/series2/4.png 800 400 %}

#### Install RVM

  Now, the below command installs the latest version of the rvm and does all the depandancies.

  {%codeblock%}
    cat rvm.sh | bash -s stable
  {%endcodeblock%}

  {% img /images/series2/5.png 800 400 %}
  Now, install the lates version of Ruby, using the below command



#### RVM use

  Installing RVM to /home/username/.rvm/

  Adding rvm PATH line to /home/username/.profile /home/username/.mkshrc /homeusername/.bashrc /home/username/.zshrc.

  Adding rvm loading line to /home/username/.profile /home/username/.bash_profile /home/username/.zlogin.

  Installation of RVM in /home/username/.rvm/ is almost complete:

  * To start using RVM you need to run
  ```
  source /home/username/.rvm/scripts/rvm
```
in all your open shell windows, in rare cases you need to reopen all shell windows.

#### Install latest Ruby

  ```
    rvm install ruby --default
  ```

  {% img /images/series2/7.png 800 400 %}


#### check the ruby Version

  {%codeblock%}
    ruby -v
  {%endcodeblock%}

  {% img /images/series2/8.png 800 400 %}

## Install Postgres

  execute the below commands one by one

  {%codeblock%}
    sudo sh -c "echo 'deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
    wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
    sudo apt-get update
    sudo apt-get install postgresql-common
    sudo apt-get install postgresql-9.5 libpq-dev
  {%endcodeblock%}

  {% img /images/series2/9.png 800 400 %}
  {% img /images/series2/10.png 800 400 %}
  {% img /images/series2/11.png 800 400 %}
  {% img /images/series2/12.png 800 400 %}
  {% img /images/series2/13.png 800 400 %}

#### Roles in postgres

  by default postgres create a root user called role here is "postgres"

  to use that

  {%codeblock%}
    sudo -i -u postgres
  {%endcodeblock%}

  {% img /images/series2/30.png 800 400 %}

#### Create a New Role

  We entered to the console, now, create a new Role.

  {%codeblock%}
    createuser --interactive
  {%endcodeblock%}

  {% img /images/series2/15.png 800 400 %}

now, the user is created, now to check that type

  {%codeblock%}
    psql
  {%endcodeblock%}

when the console comes, then type

  {%codeblock%}
    \du
  {%endcodeblock%}

  {% img /images/series2/16.png 800 400 %}

#### To set Password for User

go to the psql by command

  {%codeblock%}
    sudo -u postgres psql
  {%endcodeblock%}

  {% img /images/series2/17.png 800 400 %}

  type

  {%codeblock%}
    \password user_name
  {%endcodeblock%}

  {% img /images/series2/18.png 800 400 %}

this is the end of series, will post more in another series

all set. thanks guys, comment if any error or doubt happend.
