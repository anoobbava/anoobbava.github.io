---
layout: post
title: "Implement Likes rails With AJAX using Acts as votable Gem"
date: 2018-03-15 12:24:19 +0530
comments: true
categories: [Ruby, AJAX]
published: true
---

### Why this Gem
  Thanks to Ryan T, without his idea, it will be diffcult. Acts as votable is a gem deals with voting mechanisms, like and unlike things etc, pretyy cool isn't it right.This blog is only a simple idea to use this gem, for more advanced ones you can go to the

  [github link](https://github.com/ryanto/acts_as_votable)

### Add Gem to Rails Project

  to fetch the latest version, [rubygems acts as votable](https://rubygems.org/gems/acts_as_votable)
  copy the gem and add to our project Gemfile

  {% img /images/acts_as_votable/1.png 400 200 %}

  then run

  ```
    bundle install
  ```
### create a migration for the  acts_as_votable

  In order to save the votes and its depanancies, needed a table, Thanks to Gem, they will create automatically when we run the migration, Run the command in the Terminal.

  ```
  rails generate acts_as_votable:migration
  ```

  ```
    bundle exe rails db:migrate
  ```


### Use case in Project

  The Project here I have here is the blog project which contains the Article model and User model. The User able to like an article. By Using AJAX , there is no need to refresh the page. so in the Article model add

  ```
    acts_as_votable
  ```

  {% img /images/acts_as_votable/2.png 600 200 %}

  Also add the voter to User model Also,

  ```
    acts_as_voter
  ```

  {% img /images/acts_as_votable/3.png 600 100 %}

### ADD the Corresponding Action in the controller

  In order to work, we need to create an action in the controller, here in my case, there is ArticlesController, what we are doing is create a new action called like

  {% img /images/acts_as_votable/4.png 600 100 %}

  Will explain the codes here below
  -----------------------------------

  since we are only implementing here, we need to add the table which user likes the article, for that , the built-in from gem is the "upvote_from".
  current_user is the devise_helper to fetch the logined user.
  @article is an instance of the article page.

### ADD the Routes

  Since the like is the custom action, what we need is the new routes in the article and it is a PUT Action.Also each like belongs to a single article, so we are implementing is the member action under the articles

  {% img /images/acts_as_votable/5.png 500 100 %}


### Create a template corresponding to Like action

  We are using AJAX to update the count of likes, this will need a like.js.haml needed inside app/views/articles/

  contents are

  {% img /images/acts_as_votable/6.png 600 100 %}

  Right now, the code does not make any sense. since I am following HAML logic, a little bit different than ERB ones.
  the #like-count is the div id, what we have used here is , after liking, we updated the count of likes to #like-count div.
  get_upvotes.size is the helper to fetch the count of likes for the corresponding article.

### Like button in the UI

  will check the routes is everything all okay,

  {% img /images/acts_as_votable/7.png 700 100 %}

  Ahh!, All set, now add the route path in the page where like button needed, I have added a like.png image in assets to look like social media button. also a CSS class to reduce the image size, if you needed add that or just discard that.

  {%img /images/acts_as_votable/8.png 700 100 %}

### ADD the Div id to update the count of like

  We have mentioned and id = #like-count in the lik.js.haml, need to add that in any place we can show the count of like. In my example, i have a glyphicon to show that before that i added it like below.

  {% img /images/acts_as_votable/9.png 700 100 %}

  Will Explain the codes below
  -----------------------------
  when the page intially loaded acts_votable gem called "get_upvotes" will fetch all the likes and show in the page, after that, if any likee from user, then the system Will AJAX and there by calling the like.js.haml and update the new count via AJAX.

  All completed, now the output, will show you, like button

  {% img /images/acts_as_votable/10.png 200 100 %}

  like count image

  {% img /images/acts_as_votable/11.png 300 100 %}

   Note: the count shows as 2 because, I liked 2 times from 2 different accounts, actually there will like only one like per account per article, the gem is intellegent as it is ,again Thanks to Ryan T for this,
   If you have show stoppers, please check the code in

  [github](https://github.com/anoobbava/wiki_clone_app)

  thanks Guys.
