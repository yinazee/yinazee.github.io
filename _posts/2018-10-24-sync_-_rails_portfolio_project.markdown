---
layout: post
title:      "SYNC - Rails Portfolio Project"
date:       2018-10-24 08:05:43 -0400
permalink:  sync_-_rails_portfolio_project
---

![](https://i.imgur.com/7mWgxOY.png)

I went in with a big ambition of creating an application where people could choose the time and date of when they would meet with up to 7 dates as choices. Found out someone's already created that idea. (Check out Doodle.)

I was trying to emulate some aspects of it but it requires Javascript and I will be learning that next in the curriculum.

Using this app is a great way to schedule a meet up among friends, family, coworkers. The goal is where each person gets to pick as many available times they want. The date that gets most picked will be the date. It's an end to a lot of back and forth in group chats.

I've created a quick cheat sheet for when I need to create a new rails app again, I'll be able to do so in the most simple instructions possible:

1.	Create repo on your github

2.	Then on your terminal:

     a.	$ rails new sync
		 
     b.	now push to your existing repo
		 
       i.	$ git init

       ii.	$ git add .

       iii.	$ git commit –m “First commit”

       iv.	$ git remote add origin https://github.com/yinazee/sync

       v.	$ git push –u origin master
			 
     *	Trouble shoot

            i.	If you are unable to push:
           1.	$ git pull
           2.	$ git push (if it still doesn’t work then do git push –f)
           3.	Add your gems, copy a gemfile from a previous project

3.    Follow this [lab](https://learn.co/tracks/full-stack-web-development-v6/rails/authentication/omniauth) to complete social media login
  To use login link: <%= link_to (‘Log in with Facebook!’, ‘/auth/facebook’) %>
	Must remember to add .env to your .gitignore file

4.	Now set up your databases

============================================

## Sync  - Setting up your models
#### So after setting up the basic foundation of my rails app, I set up what models I need and their relationship to each other

So I wanted to create a user model and each model will take on 2 hats or 2 other roles.  They could be a host or a guest. So everytime a new user is initiated, a host and guest instance gets created by association. Hence:


=======

<b>User</b>

has_one host

has_one guest


=======


Now to set up the Host model and the Guest model to reflect this:

=======

<b>Host</b>

belongs_to user

<b>Guest</b>

belongs_to user


=======


Now it's time for a join table model. So the main purpose of this application is so that a host can create events and invite guests. I need a join table that keeps track of the unique relationship between a guest and an event. Hence:

======


<b>Host</b>

belongs_to user

has_many events

<b> EventGuest </b>

belongs_to event

belongs_to guest

<b> Guest </b>

belongs_to user

has_many event_guests

has_many events, through: event_guests

has_many hosts through events

<b>Event</b>

belongs_to host

has_many event_guests

has_many guests, through: event_guests

=======

As I'm writing this entry, I felt like I should have combined the roles of User, Guest and Host to just User. It makes for better data management. I think for the sake of streamlining and simplifying information, less is more. For my application, I think it's acceptable to say that a User can create events and be invited to events.  This thought is still not concrete but surely after spending quite amount of time figuring out the relationships between the models and then 



	 ## talk about what a user can do
	 ## talk about what an invited guest can do
	 ## talk about how events#index page is organized
	 ## talk about challenges
			 
Sources:

'https://rubygems.org'
For this project, I added:
    Simple Calendar Gem
    Pry
		Bootstrap
		Autoprefixer-rails
    Social media login gems (Facebook)
	   	i.	gem ‘dotenv-rails’
		  ii.	gem ‘omniauth’
      iii.	gem ‘omniauth-facebook’
			 
[Scope Methods verses Class Methods](https://www.justinweiss.com/articles/should-you-use-scopes-or-class-methods/)
