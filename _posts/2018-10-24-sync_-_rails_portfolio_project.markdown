---
layout: post
title:      "SYNC - Rails Portfolio Project"
date:       2018-10-24 08:05:43 -0400
permalink:  sync_-_rails_portfolio_project
---

![](https://i.imgur.com/7mWgxOY.png)

Sync is an application where Users get to create events.  It is a great way to schedule a meet up among friends, family, coworkers. 

I went in with a big ambition of wanting to create an application where people could choose the time and date of when they are free to meet. Found out someone's already created that idea. (Check out Doodle.) So ultimately, the goal is for each host to pick a range of dates and times and it will be displayed like a time table.  Then each invited guest gets to pick as many available times they want. The date that gets most picked will be the date for the event. It puts an end to a lot of back and forth in group chats.

I was trying to emulate some aspects of it but it requires Javascript and I will be learning that next in the curriculum. So this is still an ongoing project but it fulfills the requirements of my rails portfolio project so far.


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
*It may be helpful to have a peer review these model relationships before you do your migrations.

## The User Model
So to recap, a User takes on 2 additional roles. They have a host_id to create events with and a guest_id, so that they could be invited to an event.  The user itself could not edit their information----

As I'm writing this blog entry after I 'finished' my project, I have just made the decision that a user will be unable to delete their account.  A lot of the models are dependent on the User model.  If a User gets deleted, the events where that User is invited to, will crash, unless I put in a condition to prevent that.  But more importantly, the events that the User created in the past will be deleted too.  And with that, I would have to delete all the EventGuest models that have been invited to those events.  That wouldn't make sense. So I removed the User delete function.

## The Guest Model verses EventGuest Model
We can access the EventGuest object through @event.event_guests and it will output a list of all the guests invited to that particular event.  Here is the basic difference:

--To access the guest's name:
Via Guest Model: @event.guests.first.user.name
Via EventGuest Model: @event.event_guests.first.guest.user.name

Though any changes made to an invited guest, should be addressed via the EventGuest model.

To display a list of guests in particular to that event, we need to access the joint table model, we would be able to identify which event (by event_id) and who (guest_id) will be going.  It also has a 'rsvp' attribute which is set to a boolean type, that will be able to track who is going to the event or not.

User also may not edit the guest list after they created a new event.  

* Ideally, an invited guest would get a notification that they have been invited to an event.  But it would be confusing if the event no longer shows up on their 'Events You Have Been Invited to' list.  It may also not be permissible in real life parameters for someone to be invited and then not invited.  But this thought will be revisited, too many options for a User may not be a good thing either.  If I do want the guest list to be editted, the rsvp function would expire after a set amount of time.  But for now, we are just going to assume all guests will not be attending and if they attend, they will have to check the 'Yes' box to submit.  Once this has been submitted, it can not be editted by the User.  


	 ## How the Events#Index Page is Organized
	 When an event gets created, Users invite guests.  This event will then show up on a guest's Event's Index page.  To access events that a User has been invited to, simply access @user.guest.events.  And for a list of events that a User has created, access @user.host.events.  A guest should never be able to edit or delete an event.
	 
	 
	 ## Challenges
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
