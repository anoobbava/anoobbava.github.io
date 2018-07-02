---
layout: post
title: "GCP:1 Rails App Deployment using GCP"
date: 2018-04-11 00:32:23 +0530
comments: true
categories: [gcloud, Ruby, Rails, Deployment, GCP]
---

## Deployment using GCP

{% img /images/gcp-1/0.png 800 300 %}

This will be a series of tutorials in which step by step deployment of a ROR project in Google Cloud or GCP. From here onwards it is mentioned as GCP.

## Why GCP

I am a huge Fan of Open Source Technologies, I have used the Heroku Free Tier, RedHat,Engine Yard Also. I have been tried to use the AWS for a long time. The issue with AWS is that it has free tier but needed credit card to sign-up.Also In the case of heroku, is a PAAS Application and all the process are automated and customisation is less.

#### Pros of GCP

1. comes from Google , oh! Yaaah
2. No need of credit Card
3. Need only debit card with VISA or MASTER CARD.
4. gives us the $300 credit once signup.
5. $300 credit for 12 months

`Google Cloud Platform, offered by Google, is a suite of cloud computing services that runs on the same infrastructure that Google uses internally for its end-user products, such as Google Search and YouTube.`


We have explained here is the basic use case to deploy the app, for more details, please refer the official guide.

### signup

1. go to [got to GCP](http://www.cloud.google.com/)
2. signup with your email
3. add the payment details; dont worry, only debit Card needed, they is no harm because of this, they dont take amount from account unless you have to upgrade the account.

Note:
  I have used ICICI Debit Account, and they deducted 50Rs from my account to verify and returned the amount. So No Worries, only i got is a 2 rs for MY OTP.

{% img /images/gcp-1/0_1.png 300 600 %}

### Create a Project

Now, create a Project.

{% img /images/gcp-1/1.png 800 300 %}

give a name for the project

{% img /images/gcp-1/2.png 800 400 %}

### Create an instance

Now the process is create the instance. Instance is something like a virtual machine. This can be fetched from the Compute Engine. Example instances are production, staging etc.

{% img /images/gcp-1/3.png 800 400 %}

Now, add some details to complete the instance creation.

{% img /images/gcp-1/4.png 800 400 %}

I have used is the ubuntu 16.04, you can choose your BootDisk.

Now, important part, need to link the SSH Key to the GCP.

{% img /images/gcp-1/5.png 800 400 %}

click on the create instance

### Link SSH to GCP

go to the metadata and click on the SSH keys and ADD,then paste the public key to there.

{% img /images/gcp-1/13.png 800 400 %}

In order to do that, need to copy the public key

1. Show the available SSH keys

{%codeblock%}
  ls -al ~/.ssh
{%endcodeblock%}

{% img /images/gcp-1/6.png 800 400 %}

2. copy the desired public key

{%codeblock%}
  head ~/.ssh/id_rsa.pub
{%endcodeblock%}

{% img /images/gcp-1/7.png 800 400 %}

3. Add the public Key to the GCP

{% img /images/gcp-1/8.png 800 400 %}

### Create a Pem File

because of security concerns and multiple connectivity of instances, We need to generate the pem file from the public key, this is achieved by using.

open a new terminal and run the below code.

{%codeblock%}
  ssh-keygen -f ~/.ssh/id_rsa.pub -m 'PEM' -e > public.pem
{%endcodeblock%}

{% img /images/gcp-1/9.png 100 50 %}

Now the code will generate the pem file in the place of terminal points to , in my case it is home path

Now change the permission of the pem file, by below comand

{%codeblock%}
  chmod 600 public.pem
{%endcodeblock%}

### connect the GCP using SSH

{%codeblock%}
  ssh -i public.pem user_name@external_ip
{%endcodeblock%}

{% img /images/gcp-1/14.png 800 300 %}

user_name is the name which is shown when we copy the ssh key, here irfana_anoob is the user_name

external-ip is the IP which is given when we create the instance

{% img /images/gcp-1/15.png 800 300 %}

this is the Series1, will be posting more posts on this Also.

all set. thanks guys, comment if any error or doubt happend.
