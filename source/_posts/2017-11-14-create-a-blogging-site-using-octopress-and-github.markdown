---
layout: post
title: "Create a Blog with Octopress"
date: 2017-11-14 19:20:57 +0530
comments: true
categories: [Ruby, octopress]
published: true
---

### Why Blogging

Most of us are very much interested to write the blog to share what we think and to express our ideas to the world. But in reality, it won't work. Sometimes Lazy attitude and lack of knowlegde about how to blog. Thanks to Ruby We have Awesome tool called Jekyll to blog.

### What is a Jekyll.

{% img /images/octopress/jekyll_image.png 600 300 %}

Jeykyll is a static, simple blog aware site generator out of ruby. It is the one of the most trending repos of ruby in gthub.There are a lot of customisations in the jekyll; when we look it for the first time, we dont understand it very well.Same experiance for me too, but I don't give up. I learned more about that and I came up with Octopress.

[github link for jekyll](https://github.com/jekyll/jekyll)


### What is Octopress

First of all, Octopress is a blogging framework for hackers built on top of jekyll. It has awesome theme with nice understanding workflow for a newbee.

### What we need

1. Github account
2. undertstanding about Ruby Programing language
3. YML and kind of thigs
4. Any IDE like Sublime Text


### Setup Github

The reason I like GitHub it is super cool and provides free services. We can create public repos free and there is a place for static page too. In order to that need to create a repo name like this
github-user-name.github.io.
github-user-name is the username of your GitHub. Suppose your username is awesome.Repo name is awesome.github.io

#### Create new repository
  for test purpose used a repo named user-name.github.io, here i have used awesome.github.io

  {% img /images/octopress/1.png 600 300 %}

make sure it is a public repository and create repository.
since already have a github.io in my account, I cant use that refer to this answer in stackoverflow.
[refer link for details](https://stackoverflow.com/questions/15563685/can-i-create-more-than-one-repository-for-github-pages).All done from th github account.

### Setup the octopress.

[Refer using the link](http://octopress.org/docs/setup/)

1. before installing octopress, make sure we have the ruby, git installed in our system.

2. clone the octopress using below git url
```
git clone git://github.com/imathis/octopress.git awesome_blog
```

3. Change to the directory awesome_blog

{% img /images/octopress/2.png 600 300 %}

4.set the ruby version using rvm

{% img /images/octopress/3.png 600 300 %}

5.install the bundler using below command

```
gem install bundler
```

6.then bundle install

{% img /images/octopress/4.png 600 300 %}

7.octopress is bundled with default theme, we can customise later, for now, we will use the default theme.

```
rake install
```
{% img /images/octopress/5.png 600 300 %}

### linking GitHub account with Octopress

To do that we need to run this code.

```
rake setup_github_pages
```
It is actually a rake task will ask the GitHub URL Repo.
here we have 
```
git@github.com:anoobbava/awesome.github.io.git
```
Also it creates a new remote called octopress. A new branch source is created which contains the updations from our side where as the master contains the static page.

{% img /images/octopress/6.png 600 300 %}

Now the process we need to generate a static page from this code, this can be achived using below command.
```
rake generate
```
push this generated static site to the github using the command.
```
rake deploy
```

Now the page is deployed, but the changes are still in the local machine we need to push to source branch.
Which is achieved by 
```
  git add .
  git commit -m 'commit msg'
  git push origin source
```
*Note to remember:* The static page deployed in the master branch and the code that we changed need to be pushed to source branch.

when we done any changes, and need this change in the production, so the below commands to be executed after every changes occurs.
```
  rake generate
  rake deploy
```
7.png

{%img /images/octopress/7.png 600 300 %}

I have an existing user-name.github.io with account, So i can't create an another one. So I will be explain about the existing github.io account.

### Write a Blog using Octopress
 
For that I have switched to my account, you guys can use the user-name.github.io account.

Create a new post using below command.

 ```
 rake new_post["post_name"]
 ```

 Before creating a blog post, We need to understand that this rake will generate a file in a markdown format and this markdown file will be end with YYYY-MM-DD-post-title.markdown and the path is in source/_posts.

 Here I am creating a blog of how to create a blog using octopress and github.

{%img /images/octopress/8.png 600 300 %}
 
The above rake will create a YAML based file which contains below details
```
---
layout: post
title: "Create a Blogging site using Octopress and GitHub"
date: 2017-11-14 19:20:57 +0530
comments: true
categories: 
---
```

All the things are bit straight forward ,only doubt comes from comments: true and the categories. Comments will be discussed later, categories means which all categories this blog will comes, we can provide multiple ones, here I am using below ones only.

```
categories: [Ruby, octopress]
```

Now we need to test what is the result is going to come, achieved by using below commands,

```
rake generate # will make the static file
rake preview # generate a localhost:4000 web browser and we can preview file.
```


{%img /images/octopress/9.png 600 300 %}

### Browser result

{%img /images/octopress/10.png 600 300 %}

If we don't want the file to be published and we need to do some path works and design and something and you are in the middle of the blog, then set the 

```
published: false
```
to the blog post and it will not publish the page to the blogging site 
example:
```
blog yml
layout: post
title: "Create a Blogging site using Octopress and GitHub"
date: 2017-11-14 19:20:57 +0530
comments: true
categories: [Ruby, octopress]
published: false
```
then refresh the browser, Hooray the new blog is disappeard.

{%img /images/octopress/11.png 600 300 %}


### Sharing code and highlights

we can use using tilde "~" symbols for this option.The below option is achived using 3 tilde in one line, then in the next line data and in the next line 3 symbols

```
You are Awesome
```
{%img /images/octopress/12.png 300 100 %}


#### Display images inside the blog

1. Place the image in to the blog path/source/images/
2.better to keep a folder for each blog posts inside the images/

```
syntax: {"%img /images/blogfolder/image_name size %"}
example : {"%img /images/octopress/23 600 300 %"}
```
Since we cant use the correct syntax, because octopress executed as command, so Please remove the double quotes inside the braces before using the above syntax.

#### Gist inclusion

If we have more code examples, the preferred is the gist inclusion. Gist is a place where we can store the chunks of code for later use, like the commons rspec for a controllers or ActiveRecord queries etc.
It is Free and from github. Go to the [ink](https://gist.github.com/) and create a gist and add to the blog. copy the embeded path starts with the "script src" and paste inside the blog like below

```
<script src="https://gist.github.com/anoobbava/e197d468b7f8d8cc3e404fed9ced1b38.js"></script>
```

All of configs are not covered here, Please refer the official octopress blog for details. Happy Blogging all of you, dont forget that once you completed, then do the below steps to complete

```
rake generate
rake deploy
rake add .
git commit -m 'Completed the blog about the octopress'
git push origin source
```