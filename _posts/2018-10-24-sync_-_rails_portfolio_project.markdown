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
			 
     *	Trouble shoot:
     * If you are unable to push:
     * $ git pull
     * $ git push (if it still doesn’t work then do git push –f)
     * Then finally copy the basic gemfile from a previous project and add your custom gems

3.    Follow this [lab](https://learn.co/tracks/full-stack-web-development-v6/rails/authentication/omniauth) to complete social media login
  To use login link: <%= link_to (‘Log in with Facebook!’, ‘/auth/facebook’) %>
	Must remember to add .env to your .gitignore file

4.	Now set up your databases

============================================

## Sync  - Setting up your models
#### So after setting up the basic foundation of my rails app, I set up what models I need and their relationship to each other

I always set up my models on paper and draw out their relationships.  
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

As I'm writing this entry, I felt like I should have combined the roles of User, Guest and Host to just User. It makes for better data management. I think for the sake of streamlining and simplifying information, less is more. For my application, I think it's acceptable to say that a User can create events and be invited to events.  

## The User Model
So to recap, a User takes on 2 additional roles. They have a host_id to create events with and a guest_id, so that they could be invited to an event.  The user itself could not edit their information----

As I'm writing this blog entry after I 'finished' my project, I have just made the decision that a user will be unable to delete their account.  In particular to my application because a lot of the models are dependent on the User model.  If a User gets deleted, the events where that User is invited to, will crash, unless I put in a condition to prevent that.  But more importantly, the events that the User created in the past will be deleted too.  And with that, I would have to delete all the EventGuest models that have been invited to those events.  That wouldn't make sense. So I removed the User delete function.

## The Guest and EventGuest Model
So as we are setting up the guest model, each guest id is created everytime a user is created.  This is so each event gets a list of guest_ids.  We can access it by entering @event.guests.  But if we want to invite, uninvite and find out if they rsvp'ed, we need to access @event.event_guests.  The event_guest models are unique because it is a combination of the event_id and guest_id.





	 ## talk about how events#index page is organized
	 ## talk about challenges
	 ## talk about ongoing challenges and questions
	 -should a users be able to delete their accounts.
			 
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
