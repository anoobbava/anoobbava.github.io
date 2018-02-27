---
layout: post
title: "Implement Rspec in ROR Project"
date: 2018-02-27 16:44:30 +0530
comments: true
categories: [Ruby]
published: true
---

## Rspec, A Brief
 
 Below is the some syntaxes and errors i have encountered when using rspec, I have shared here for every ones' use.

### install rspec
  install the rspec gem using the below command

  ```
  gem install rspec
  ```

### create a test Group

  ```
  group :test do
    gem 'codeclimate-test-reporter', '~> 1.0.0'
    gem 'database_cleaner', '~> 1.5'
    gem 'factory_bot', '~> 4.8', '>= 4.8.2'
    gem 'factory_bot_rails'
    gem 'faker', '~> 1.6.1'
    gem 'rails-controller-testing', '~> 0.0.3'
    gem 'rspec', '~> 3.6'
    gem 'shoulda-matchers'
    gem 'simplecov'
  end
  ```
  the gem factory_girl is deprecated right now, so we are using the factory_bot instead.

### Add rspec-rails to the Development Group

  ```
  gem 'rspec-rails'
  ```
  Now we need to add the development, test group

### Intialise the folders for Rspec

  achieved using the below command

   ```
   rspec --init
   ```

### Require rspec/rails to spec helper

  ```
  require 'rspec/rails'
  ```

   need to add above command to the spec_helper

### You are Go

  All set, now delete the test/ folder in the project and create the specs in models and ccontrollers

  to generate rspec file for existing controller

  ```
  rails generate rspec:controller Controller_name
  ```

  to generate rspec file for exising model

  ```
  rails generate rspec:model model_name
  ```

### setup test database

  Do the below step only if you don't have the test database created

  ```
  rake db:test:prepare
  ```

### Why we need the database cleaner

  Is a useful tool to clear the dB from the test database. for that need to use the database_cleaner gem in test group.

  1. add the gem

    ```
    gem 'database_cleaner'
    ```
  2. require in spec_helper

    ```
    require 'database_cleaner'
    ```

  3. add the tables where clearing is needed

    ```
    DatabaseCleaner.strategy = :truncation, { :only => %w[users] }
    ```
    here users is one table, multiple tables can be added using comma
  4. Call the action

  add the below line where we need to clean the dB

  ```
  DatabaseCleaner.clean
  ```
  Note: in psql manually create test database  and do rake db:migrate RAILS_ENV=test

### Important Points to  remember

  1. To clear all the data

  add the below line to the spec_helper

  ```
  config.after :all do
   ActiveRecord::Base.subclasses.each(&:delete_all)
  end
  ```
  2.To view the console of test dB

  ```
  rails c test
  ```
  3. If below Error comes up

    undefined method `sign_in' for #<RSpec::Core:

    Solution
    ----------
    add below line to spec_helper

    ```
    config.include Devise::TestHelpers, type: :controller
    ```
4. If below error pops Up

    rmed176lt@RMED176LT:~/ror/12-week/wiki_clone$ bundle exec rails generate rspec:install
    Running via Spring preloader in process 10346
    Could not find generator 'rspec:install'. Maybe you meant 'devise:install', 'responders:install' or 'simple_form:install'
    Run `rails generate --help` for more options.

    Solution
    ------------
    [visit link for SO answer](https://stackoverflow.com/questions/39542169/rails-5-could-not-find-generator-rspecinstall/39542170)

5. If below error pops up

  1) ArticlesController redirect to user signin
       Failure/Error: get :index
       
       NoMethodError:
         undefined method `get' for #<RSpec::ExampleGroups::ArticlesController:0xb8c4f8c>
         Did you mean?  gets
                        gem
       # ./spec/controllers/articles_controller_spec.rb:6:in `block (2 levels) in <top (required)>'

  Finished in 0.00479 seconds (files took 4.41 seconds to load)
  1 example, 1 failure

  Failed examples:

  rspec ./spec/controllers/articles_controller_spec.rb:5 # ArticlesController redirect to user signin


  Solution
  -----------
  1. need to add require 'rspec/rails' in spec_helper
  2.  if wont work then add below line
  ```
   config.infer_spec_type_from_file_location!
   ```
  for me, 2 nd one is not required.


### below is sample spec_helper.rb
<script src="https://gist.github.com/anoobbava/27255d8052d7b8d5ac095f511e6e242b.js"></script>