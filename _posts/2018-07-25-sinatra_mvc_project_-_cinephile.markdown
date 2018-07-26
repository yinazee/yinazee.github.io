---
layout: post
title:      "Sinatra MVC Project - Cinephile"
date:       2018-07-25 02:09:49 -0400
permalink:  sinatra_mvc_project_-_cinephile
---

![](https://i.imgur.com/rLIOHO6.png?1)

**So this is how I started on the project** 

I had a few ideas in my head before I started the project.  I wrote them on a post it and kept them in the back of my head.  So as I was working on the labs before it, I would take notes on what features I need from the labs, so that when I start the project, I know exactly which previous labs to go back to when I need reference.

Then I did a 1 on 1 meeting with Howard DeVinnish who leads the study group for Sinatra, ActiveRecord, SQL, and ORM.  I highly recommend it to students who do not come from a coding background.  I had a list of questions to ask him, but he took me a step back and asked me exactly what is Sinatra and Active Record? I have read about it before but I was caught off guard and could not remember, which means, I didn't fully understand the concept if I couldn't verbalize it. It pays to refresh your memory of the following key questions before you meet with Howard.  

**What is the difference between website and web application?**
So WAF (Web Application Frameworks) allows a website to be dynamic so that it could create, store, delete as many user accounts, blog posts, data, etc.  WAF alleviates a lot of the website's repetitive tasks by following RESTful conventions, a concept created by Roy Fielding.

**What is Sinatra?**
"[Sinatra ](https://learn.co/tracks/full-stack-web-development-v5/sinatra/sinatra-basics/what-is-sinatra)is a Domain Specific Language implemented in Ruby that's used for writing web applications. Created by Blake Mizerany, Sinatra is Rack-based, which means it can fit into any Rack-based application stack, including Rails. It's used by companies such as Apple, BBC, GitHub, LinkedIn, and more."  Sinatra is a great way to start to learn about the 'magic' of the web.  This is where you will have to manually write the routes that hit up your designated view files for the users to CRUD (create, read, update, delete). Users of most websites will almost always need to create an account, log in, log out, etc. and those actions, leads to routes that render a view page; a view page is where the models or category of certain information gets CRUD.


**What is MVC?**
As we learned from SQL about databases, MVC stands for Model, Views, Controller. Write down models you need for your website and create migrations for them. I spent 3 hours (pencil highly recommended) and just draw out your models, their attributes, and then figuring out the relationships between them.  You can also do it on the computer by using [DB Browser for SQLite](https://sqlitebrowser.org/) but I prefer to do it by hand.


**Great Resource**
I thought this [pirates nested form video]([https://youtu.be/kgHN11dQ3H0](http://)) was a really good resource to set up your portfolio project. I did not find a good sinatra template, so I manually set one up and I would recommend to others to just manually set it up. It doesn't take that long and it helps greatly with knowing how all the nooks and cranny works before the abstraction.

**Fun Challenge**
Google is your friend. I've never done a drop down select menu before. But I know the website would be better with one and so I googled on how to build one. And I wanted to get the top directors in the industry in that select menu for users to pick.  Thanks to my experience with the CLI project, my scrapping skills are top-notch. Then it comes down to cleaning up the data and then I had to alphabetize them. But then the next challenge was, how can I get the check mark to preselect the first director? Ok, create the first entry as blank.  Ok, but how do we get the checkmark to show on the director you chose, on the edit page? And this was the hardest part: getting the show page to show the newly selected director. Ok, 10 hours of coding later, done. Ok but now how do I get a newly created director to show in the list in its correct abc order and not just at the bottom? Still on it.

**You: Before and After**
I became really good at binding.pry.

**Overall Thoughts**
I was going through the hurdles just like I did when I was working through the CLI Data Project. I had negative thoughts creep in my head that I wasn't going to get this, that I'm not smart enough, and then I stop to tell myself out loud that 'You can do this. It's only a matter of time. You can do this.' followed by visions of a better work/personal life. I would stay up till 3/4am and get up a few hours later. I find myself more focused, later on in the night.

I spent 3 weeks on this project while working full time; an extra 8  more than what I had planned on finishing this project. I submitted the project but there are parts of it I would love to revisit and work on.)

