---
layout: post
title: "delayed job with recurring option"
date: 2018-05-29 22:37:41 +0530
comments: true
categories: [ruby, rails, Delayed job ]
---

## delayed job recurring


### Requirement

I have an app called clone app and the user will update some information to the table call user_informations. Our requirement is to copy this data to another table user_information_backups. It will be a background job. But we dont want to run this when the user updated the user_informations, instead what we are planning is to do the backup in each 5 mins. when the backup is completed, mark the cloned one master as flagged to restrict one information to be taken more than one.

[app link](git@github.com:anoobbava/delayed_job_recurring_example.git)

### 1. create an app user_clone

{% img /images/dj/1.png 800 500 %}

used the database as mysql in dev, since I have sqlyog to installed for proper UI View and understanding.

database is mysql , we can understand from the gemfile.

{% img /images/dj/2.png 800 500 %}

my database.yml file is attached below

{% img /images/dj/3.png 600 200 %}

Need to create the database

{% img /images/dj/4.png 800 500 %}

now the database is shown in the sqlyog tool

{% img /images/dj/5.png 400 300 %}

create the model UserInformation

{% img /images/dj/6.png 900 500 %}

update the user_informations migration

{% img /images/dj/7.png 900 500 %}

migrated the file

{% img /images/dj/8.png 900 500 %}

created the model UserInformationBackup

{% img /images/dj/9.png 900 500 %}

display the table in sqlyog

{% img /images/dj/10.png 400 200 %}

Now, we need to generate the controller

{% img /images/dj/11.png 900 500 %}

Do the crud operations.

controller code is attached here below,

<script src="https://gist.github.com/anoobbava/b1a856e6d9b732cbd1565e5a643714ce.js"></script>

routes file

{% img /images/dj/12.png 300 100 %}

index page

{% img /images/dj/13.png 900 500 %}

new Page

{% img /images/dj/14.png 900 500 %}

update the migration to fetch only the unselected ones

is_selected to user_informations , default value: false

{% img /images/dj/15.png 900 500 %}

{% img /images/dj/16.png 900 500 %}

add a custom action in controller and route

```
  get 'users/display_backup', to: "users#display_backup"
```

action in controller

```
  def display_backup
    @users = UserInformation.all.where(is_selected: false)
  end
```

create the view part for the action

Now, the Application part completed, moving to our delayed_job and its works.

### Delayed Job
  install delayed_job

{% img /images/dj/17.png 600 300 %}

```
rails generate delayed_job:active_record
```

{% img /images/dj/18.png 900 700 %}

```
rails db:migrate
```
{% img /images/dj/19.png 900 600 %}

set the below config in application.rb

```
  config.active_job.queue_adapter = :delayed_job
```

{% img /images/dj/20.png 900 700 %}

Now the backup process code explained

```
  def self.intiate_backup
    user_details = UserInformation.fetch_details
    if user_details.present?
      instance_data = []
      user_details.each do |user_data|
        user_backup_instance = UserInformationBackup.new
        user_backup_instance.first_name = user_data.first_name
        user_backup_instance.last_name = user_data.last_name
        user_backup_instance.secret_message =user_data.secret_message
        instance_data << user_backup_instance
      end
      UserInformationBackup.import instance_data
      user_details.update_all(is_selected: true)
      end
    end
  end
```
now test this process via Delayed job, we can use the rails console to check this


{% img /images/dj/21.png 900 500 %}

{% img /images/dj/22.png 900 600 %}

now the entry got added, we can this delayed job using the command

```
  bundle exec rails jobs:work
```

{% img /images/dj/23.png 900 600 %}

one issue we have encountered is we have used model.import , which is coming from

```
gem 'activerecord-import'
```
it is not added here, need to add the gem and do the bundle install
```
  gem 'activerecord-import', '~> 0.23.0'
```

{% img /images/dj/24.png 600 300 %}

and do the same same as via console and restart the delayed job

{% img /images/dj/25.png 900 500 %}

hooray , our process is done, now it will be cloned to the user_information_backups table

user_informations table

{% img /images/dj/26.png 900 500 %}

user_information_backups table

{% img /images/dj/27.png 900 500 %}

now 2 images got the same, we can't see any difference. in order to check the difference we will create a new entry to the user_informations table via UI

{% img /images/dj/28.png 600 300 %}

I have added jayakrishnan as a new entry, since this data is not cloned by the user_information_backups, it will not be there.

{% img /images/dj/29.png 600 300 %}

Now we run the DJ via console and see the magic,

{% img /images/dj/30.png 900 500 %}

{% img /images/dj/31.png 900 500 %}

{% img /images/dj/32.png 600 300 %}

Now it is the time for our cookery show, we will do the delayed job recurring.

add below gem to the gemfile.

```
  gem 'delayed_job_recurring', '~> 0.3.7'
```
and do the bundle install


create a folder in app/interactors.

create a file in that, we can use any file name for example, created  a file name *clone_process.rb* in

```
  app/interactors
```

```
  class CloneProcess
    include Delayed::RecurringJob
    run_every 5.minutes

    def perform
      UserInformationBackup.intiate_backup
    end
  end
```
Now, this class needs to be called for one time,  for reuse, we can use the rakes;
path: *lib/tasks/recurring.rake*

```
namespace :recurring do
  task init: :environment do
    CloneProcess.schedule!
  end
end
```
In order to run this recurring job for one time, need to call  the rake task using

```
   bundle exec rails recurring:init
```

Now

{% img /images/dj/33.png 900 500 %}

An entry is being made up in the DJ and it will be updated by the delayed_job_recurring gem

{% img /images/dj/34.png 900 500 %}

in order to test this we will create a new data via UI and wait for the DJ to pickup

{% img /images/dj/35.png 600 300 %}

but this data is not here in the clone table

{% img /images/dj/36.png 600 300 %}

after 5 minutes, DJ will pick up this.

{% img /images/dj/37.png 900 500 %}

in UI,

{% img /images/dj/38.png 600 300 %}

visit the offical doc for further details

[official doc](https://github.com/amitree/delayed_job_recurring)

Hooray, my work is done here, feel free to comment if any issue

