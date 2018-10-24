---
layout: post
title:      "SYNC - Rails Portfolio Project"
date:       2018-10-24 12:05:42 +0000
permalink:  sync_-_rails_portfolio_project
---

I went in with a big ambition of creating an application where people could choose the time and date of when they would meet with up to 7 dates as choices. Found out someone's already created that idea. Check out Doodle.

It's a great way to schedule a meet up among friends, family, coworkers. The goal is where each person gets to pick as many available times the 
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
			 
     2a.	Trouble shoot

       i.	If you are unable to push:
           1.	$ git pull
           2.	$ git push (if it still doesn’t work then do git push –f)
           3.	Add your gems, copy a gemfile from a previous project
					
					
Sources:  'https://rubygems.org'
For this project, I added:
    Simple Calendar Gem
    Pry
		Bootstrap
		Autoprefixer-rails
    Social media login gems (Facebook)
	   	i.	gem ‘dotenv-rails’
		  ii.	gem ‘omniauth’
      iii.	gem ‘omniauth-facebook’

		
3. Follow this [lab](https://learn.co/tracks/full-stack-web-development-v6/rails/authentication/omniauth) to complete social media login
  To use login link: <%= link_to (‘Log in with Facebook!’, ‘/auth/facebook’) %>
	Must remember to add .env to your .gitignore file



4.	Set up your database

       $ rails g migration CreateUsers

