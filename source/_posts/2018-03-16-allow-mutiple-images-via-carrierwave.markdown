---
layout: post
title: "Allow Mutiple Images Via Carrierwave"
date: 2018-03-16 12:59:43 +0530
comments: true
categories: [Ruby Gem]
---

### Gem intro
  In this tutoial, we are using the carrierwave gem.The aim of this tutorial is to upload multiple images for web Applications

  ```
    gem 'carrierwave', '~> 1.2', '>= 1.2.2'
  ```
  We are using this version, Add this gem to your Gemfile and do the

  ```
    bundle install
  ```

### Generate the Uploader File

  In order carrierwave to work, need an uploader Class. Which will be generated using the command

  ```
    rails generate uploader image
  ```
  Instead of image  u can give avatar or anything.As s result of the above command  a file generated called ImageUploader.rb in app/uploaders/

### Usecase of Carrierwave

  I have an Article model, and I need to upload mutliple images of the single Article. To do that, we need to generate the following

  1. ArticleAttachment Model: To save the mutliple images for the single article and article_id to denotes the images are under that article
  2. Necessory updations in the model Files
  3. Update the controller to accept multiple images
  4. Need to accept mutiple images from user
  5. show the images to user after the article creation a success!!

### Generate the ArticleAttachment Model

  To generate the model run the below command with 2 columns

  1. article_id :integer
  2. image :string

  ```
    rails g model ArticleAttachment article_id:integer image:string
  ```
  run

  ```
    bundle exec rails db:migrate
  ```

### changes in the Models
  in the Article Model, need to chnage on below,

  ```
    has_many :article_attachments
    accepts_nested_attributes_for :article_attachments
  ```

  {% img /images/carrierwave/1.png 600 100 %}

  in the PostAttachment model

  ```
    mount_uploader :image, ImageUploader
    belongs_to :article
  ```
  {% img /images/carrierwave/2.png 600 100 %}

### Changes to controllers

  Need to change the controllers in below places

  1. new Action
  2. show action
  3. create action
  4. parameters passing

#### New Action
  Need to build an instance variable to accept the article_attachments

  ```
    @article_attachment = @article.article_attachments.build
  ```
  {%img /images/carrierwave/3.png 600 100 %}

#### Show action

  To fetch all the images belongs to an article

  ```
    @article_attachments = @article.article_attachments.all
  ```
  "@article" will be set using fetch_article method

  ```
    def fetch_article
      @article = Article.find_by(id: params[:id])
    end
  ```
#### Create Action
  Need to save the data fetched from user

  ```
    if @article.save
      params[:article_attachments]['image'].each do |a|
        @article.article_attachments.create!(image: a, article_id: @article.id)
      end
      flash[:notice] = 'Article Created'
      redirect_to @article
    else
      render 'new'
    end
  ```
#### Params Passing

  ```
    def article_params
      params.require(:article).permit(:title, :content, :category_id,
                                    article_attachments_attributes: [:id, :article_id, :image])
    end
  ```
  Need to add the parameters to allow in to the system.

### Accept image from user

  We have updated the controller code, now in the View, in order to accept image from the user perspective need to update the form with below

  ```
    = f.fields_for :article_attachments do |p|
        = p.label :image
        = p.file_field :image, :multiple => true, name: "article_attachments[image][]"
  ```
  Full pciture of the form will be like below,

  {% img /images/carrierwave/4.png 700 100 %}

  Now what will happens is that in the create action, will get params with article_attachments and inside that "image" hash will have the images selected from user to be ready to be saved to the dB.

### Show the output

  Now we need to show the images after successful creation of an article. To do  that, we have updated all the images belongs to the particular to this "@article_attachments" varaiable. What we need is just iterate and print the values.

  ```
    - @article_attachments.each do |image|
            .post-image
              = image_tag(image.image_url.to_s)
  ```

thats all done, Now check it is working ,please post if any doubts or bugs encountered.

checkout my [code](wwww.github.com/anoobbava/blog_app)
