---
layout: post
title: "upload images using cloudinary in Heroku"
date: 2018-03-28 11:43:11 +0530
comments: true
categories: [herkou, ruby, cloudinary]
---

## Intro

  {% img /images/cloudinary/1.png 600 200 %}

  As discussed in the previous blogs, heroku is an awesome tool to deploy our application within minutes and no hassles. The issue is with the heroku is, for each specific applications ,need to use the add-ons. some are free and others are paid version. But to use add-on like cloudinary need to provide the credit card info, Here we are explaining how to bypass this issue

## Cloudinary

  {% img /images/cloudinary/2.png 700 300 %}


Cloudinary, as the name indicates it is a cloud space to save the images and videos. Can be used for both the web and mobile platform. Also the cloudinary provides a cool space as free tier(10GB something and 300000 photos). when We tweet about them, they provides an additional 1GB Also, Awesome right and thanks to cloudinary too.

## Implementation

1. signup with [Cloudinary](https://cloudinary.com/)

2. generate the custom cloudinary.yml via cloudinary console

3. copy to the project path

4. update the upoader File

5. Update in Herkou with ENV Variable.

6. deploy the code to heroku


### Signup with Cloudinary

Create an account with [Cloudinary](https://cloudinary.com/) using email and password.

{% img /images/cloudinary/3.png 900 300 %}

### Cloudinary.yml

If you have not seen the cloudinary.yml, dont worry, will paste my cloudinary.yml file below, Please chnage the details from the dashboard.

below is the dashboard, copy this details and replace these details to the yml file.

{% img /images/cloudinary/4.png 900 300 %}

  <script src="https://gist.github.com/anoobbava/c7fd8141c0ace8ddfac514dc145a2c3e.js"></script>

### copy to the project path

include this file in **application_root/config/**

#### update the upoader File

 in the Uploader.rb file(ImageUploader.rb or AvatarUploader.rb) change the following,

comment below codes

```
# storage :file

# def store_dir
  #   "uploads/#{model.class.to_s.underscore}/#{mounted_as}/#{model.id}"
  # end
```

### Update in Herkou with ENV Variable

Login in **herkou** dashboard and take our application and add environment variable.

{% img /images/cloudinary/5.png 800 300 %}

```
  CLOUDINARY_URL
```

### deploy the code to heroku

no worries, no need to change the code in the image_tag and upload tags, for me it is all working fine

you check in my site for the output **blog-app-bava.herokuapp.com**

code will be available in [github](https://github.com/anoobbava/blog_app)

all set. thanks guys, comment if any error or doubt happend
