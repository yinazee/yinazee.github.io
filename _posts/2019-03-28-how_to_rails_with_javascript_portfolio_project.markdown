---
layout: post
title:      "How to: Rails with Javascript Portfolio Project"
date:       2019-03-28 23:14:02 -0400
permalink:  how_to_rails_with_javascript_portfolio_project
---

For this project, I incorporated javascript methods into my exisiting Rails project, titled Sync. [Here is the link to my github repo.](https://github.com/yinazee/Sync-v2). I [duplicated](https://help.github.com/en/articles/duplicating-a-repository) the repo and retitled it to Sync-v2.

I printed out the [requirements ](https://docs.google.com/document/d/1__ggX6daBp_Lc6EWFEYXASR-UnskU5Hy9UnXGCez3mc/edit) and had it next to me while I was working on the project.   **So do not get stuck! Focus on the requirements, do not dwell!** 

Please watch these videos before starting on the project! I wish I watched these before I began my project. These are in high definition so you can see the code, the audio is clear and the instructor Cernan Bernardo gets straight to the point and makes it super easy to follow. [This video is one hour long and starts coding from scratch.](https://www.youtube.com/watch?v=oHPM0ekV7zQ) and [This video is 15min and touches basics.](https://www.youtube.com/watch?v=Yd0nH9CWWfo&feature=youtu.be).  Also, check out [Brad Smith's video and github ](http://www.smithwebtek.com/asdf)on this project.

**Ok, so to briefly explain my app:** 
Users as a host can create events and invite guests. In turn, users as a guest can be invited to an event.
The 'has-many' relationship, I will need to render for this project is that an Event has many Guests.

**First**, set up your current rails project with [Javascript gem](https://learn.co/tracks/full-stack-web-development-v6/rails-and-javascript/asset-pipeline/external-javascript-libraries) and set up your Javascript [manifest](https://learn.co/tracks/full-stack-web-development-v6/rails-and-javascript/asset-pipeline/css-manifests)
and [**REMOVE TURBOLINKS!!!**](https://www.google.com/search?q=how+to+remove+turbolinks&rlz=1C5CHFA_enUS723US723&oq=how+to+remove+turbolinks&aqs=chrome..69i57j69i60j0.4392j0j7&sourceid=chrome&ie=UTF-8)


**Second**, [render your data as .json](https://learn.co/tracks/full-stack-web-development-v6/rails-and-javascript/building-apis/using-active-model-serializer) in your browser and set up your model serializers. Serializers are basically the Javascript version of what models are in Rails.

**Third**, set up your index action in your eventscontroller.rb file.

For this project, you only need to render one model, like so:

```
respond_to do |f|
      f.html {render :index}
      f.json {render json: @events && @invites}
```

 and it will render:
 
<a href="https://imgur.com/vuzeA8g"><img src="https://i.imgur.com/vuzeA8g.png" title="source: imgur.com" /></a>

The above image shows all the events a user/host has created. But let's say you also want the events where the user/guest has been invited to. This is the .json data that shows both of those events. Modify your controller to look like this: (this is my index method in eventscontroller)

```
 respond_to do |format|
        format.html {render :index}
        format.json  { render :json => {:invites => @invites, :events => @events }}
```

so that the json will look like this in the browser:

<a href="https://imgur.com/Av2h7YM"><img src="https://i.imgur.com/Av2h7YM.png" title="source: imgur.com" /></a>

**Fourth and finally** it's time to code in your .js file. This is basically the Javascript version of your controller file.
[I find using handlebars MUCH easier. ](https://learn.co/tracks/javascript-v3/javascript/styling-and-templates/advanced-templating#) I stumbled on this by accident. I dont know how I switched my course over to Javascript V3 and was on that lesson. I didn't use handlebars on this app though because it was nearing completion and i just wanted to complete this project as I'm pressed for time.

This is what you should see when you use a debugger. After doing all of the steps above:

<a href="https://imgur.com/Z98peKy"><img src="https://i.imgur.com/Z98peKy.png" title="source: imgur.com" /></a>

**Other things that helped:**
1. [USE BREAKPOINTS!](https://www.youtube.com/watch?v=H0XScE08hy8&t=123s) Don't bother using debugger and console.log (ok, use this sparingly). Breakpoints is a major major time savor and you can see in real time, where your code/data breaks.
2. If you are really stuck, reach out to your section lead or ask questions in Slack, just reach out and someone or anyone and they will respond. Do not give up.
3. If you are able to attend any meetups or study groups or pair up. People are always willing to help. One way to know your material is if you could teach others. So pay it forward if you could as well.

My biggest issue in this project was this **error** I was getting: 

<a href="https://imgur.com/1tjde8x"><img src="https://i.imgur.com/1tjde8x.png" title="source: imgur.com" /></a>

.map() does not like the type of data that response. .map() could only iterate an array and what I was iterating over was an entire object that had keys within a key. So I had to be specific. So I changed my code from:

```
      response.guests.map(function(guest) 
```

to

```
 response.guests.map(function(guest) 
```


**Overall thoughts**
Javascript is now the third language I'm learning and I'm now starting to grasp the concept of computer langugage and the restful conventions / patterns that programmers have to code in. Barely scratching the surface of the iceberg... the journey continues...








