---
layout: post
title: "create custom error pages in rails"
date: 2018-03-22 19:54:55 +0530
comments: true
categories:
---

{% img /images/custom_error/rails_error_page.png 600 100 %}

We All know what this error page means, it is the 500 error when the internal Server issue. The problem of this issue on the server level like server Time out out or Internal issue or anything.It is not user friendly, it is the custom error page from the rails itself.

### Where is the Error Page ??

  For every Rails Project, the Page is inside  public/ folders, the files are

  1. 404.html
  2. 422.html
  3. 500.html

  this is the source of this error UI.
  We can follow 2 approaches

  1. simple one
  2. coding approach

### Simple one

  update the files with custom html and files, so the file loaded will be based on the new custom template.
  To test this, suppose your server is running on "localhost:3000" server, we can just type

 ```
    localhost:3000/500 or localhost:3000/404 or localhost:3000/422
  ```

  if it s not working, go to the "config/environments/development.rb" and make the line to "false"

  ```
      config.consider_all_requests_local = false
  ```

### Coding Approach

  We can divide this approach to 5 parts

  1. update in the Application.rb
  2. Remove the public static files
  3. Add the routes
  4. Create a new controller
  5. create the views

#### Update in the application.rb File

  ```
    config.exceptions_app = self.routes
  ```


#### Remove the static files

  All the depandant files like 404.html, 422.html, 500.html. Delete all these files


#### Add the routes

  ```
    get '/404', to: "errors#not_found"
    get '/422', to: "errors#unacceptable"
    get '/500', to: "errors#internal_error"
  ```

  this deontes the controllers and its action.

#### Create the controller

  We need to create a new controller to make this logic works that is using a contoller "ErrorsController"

  Add the action corresponding to that also,

  <script src="https://gist.github.com/anoobbava/9ed5b57e3d8bb75c77715a7057cd86b7.js"></script>

  ```
    skip_before_action :authenticate_user!
  ```

  that code is to bypass devise, or else need to login to view the errors.
#### Create the views

  create the views for the errors, so create folder named errors in app/views/

  ```
    not_found.haml
    unacceptable.haml
    internal_error.haml
  ```

  All done, you can write custom html into that, will give you a sample to work with.


  <script src="https://gist.github.com/anoobbava/f028100c28d95fd664bbf59195f26b8b.js"></script>

  it is copied from some page, I am not sure about the site, will mention thanks.




