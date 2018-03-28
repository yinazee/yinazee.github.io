---
layout: post
title:      "CLI APP - The Moment of Truth"
date:       2018-03-28 00:32:19 -0400
permalink:  cli_app_-_the_moment_of_truth
---

This has been a month and half long journey for me and I'm glad I've finally submitted my 'completed' cli (command line interface) app for review.
	 
This is a two part blog: This entry entails the technical process on how I developed my cli app. My next blog post will be about my challenges on tackling this project.

All that I've learned so far, will be tested on this project.  

*I’ve decided to scrape horoscopes- from www.Twittascope.com. 
(You can skip this paragraph if you like. Reason why I chose to scrape horoscopes...)
Generally in my experience, 3 out of 5 people memorize more or less the horoscope names according to their birth dates.  People assess other’s personalities once their birth date is asked. “Oh, you’re an aries.”, he said. Or if you're acting a certain way: “You must be a scorpio.” she said.*

*I did a term search on Google Insights and ‘horoscope’ (and its related terms) was one of the most popular search term throughout the year maintaining a value of 75 (100) being the highest.  Any term related to horoscopes hit the 100 mark the last week of December and the first week of January. Unsurprisingly, most people would still seek out how their fortune would play out for the new year even if they hold no grounds of substantial truth. Horoscopes are searched as much as the Kardashians... so, I thought it would be a fun idea to scrape horoscopes!  I chose Twittascope because of its multi-site structure and that every horoscope ends with an inspiring quote.*

**Quick Tips:**

1. Watch all of the videos on the lessons before you do anything

2. Work on a CLI outline on paper
    a. Write 'welcome' method to greet users
		b. Write a 'list' method to showcase options
		     - This is a good use for the .each iterator
		c. Write a 'display' method to capture user input
		     - This will return a result based on input. So this will be your if/else loop method
		     - Include an exit option with a goodbye message
		     - Include an error return if user inputs a typo or n/a term
    d. Call all of the above methods (in order) in a single 'overview' method that basically plays out how the          user will move on from one method to the next. This will start off the CLI so put that on top. Like so:
		
		`def self.overview
		     welcome
			  	list
				 display
			end`

3. Double check if all your 'def' and 'end' align. Make sure indentation is correct and consistent.
4. Understand the error messages. 

With just these 4 steps you can have a simple CLI running already. Then it's onto the scraping part.

I had a tough time choosing how to organize my data after I scrape. The challenge scraping from this website is that every horoscope has 3 separate links (39 separate links in total. I have to scrape from 3 different websites to gather the horoscope readings of yesterday, today and tomorrow.  So far, I'm only good at scraping all info from one website. 

Also, I was conflicted between 2 ways of organizing my data.

Should I....

Scrape data so every horoscope sign has an array of: name, yesterday, today, and tomorrow?

```
aries = [name, yesterday_horoscope, today_horoscope, tomorrow_horoscope]
gemini =  [name, yesterday_horoscope, today_horoscope, tomorrow_horoscope]
taurus =  [name, yesterday_horoscope, today_horoscope, tomorrow_horoscope]
cancer =  [name, yesterday_horoscope, today_horoscope, tomorrow_horoscope]
```

Or

Scrape data so each name, yesterday, today and tomorrow have *their* own array of: aries, gemini, taurus, etc?

```
name = [aries, gemini, taurus, cancer...]
yesterday = [aries, gemini, taurus, cancer...]
today = [aries, gemini, taurus, cancer...]
tomorrow = [aries, gemini, taurus, cancer]
```

I couldn't decide which so I was changing my code back and forth and it was a month long ordeal, with errors sprinkled on top of it.

So before I tell you which approach I chose, and after a lot of restructuring ...

This is the jist of my CLI walk-through:

**1) Greet customer**
     -List of 13 Horoscope options - including a 14th option of 'Find out what is my horoscope sign
		 -Ask customer to input that option number
		
**2) Display Today**
    -Once it captures user input, this number will return the user's today's horoscope.
		-More Options
		-It will also prompt 4 more options:
		  -display list again
			-read yesterday's horoscope
			-read tomorrow's horoscope
			-exit
			
Then I finally stuck to my guns and chose the second approach. I chose the second approach because it is better to scrape all the sub-webpages for today using nokogiri once, rather than scraping for 1 horoscope sign by using nokogiri 4 times for (name, yesterday, today, tomorrow.)  It is also much easier for a user to input a number and that number will instantly return that indexed element in all of the name, yesterday and tomorrow's arrays. 

For example: If user's horoscope sign is aries, his/her input will be 1. So name's first element is Aries. Today's first element will showcase Arie's horoscope, so on so forth.

Ok, so while scraping, I came upon another problem.  I wanted to implement the I-don't-know-my-horoscope-sign option.  If you hover the mouse over the 'don't-know' thumnail on the main-page, there is a pop-up that lists all the names with the birthdates right next to them. Like so:

```
1. Aries' Horoscope (Mar 21 - Apr 19)
2. Taurus' Horoscope (Apr 20 - May 20)
3. Gemini's Horoscope (May 21 - Jun 20)
```

This way, there's no need for a 14th option.  I'm beginning to streamline my app, I realized.  I tried for the longest time to scrape from that pop-up. But I just couldn't figure out how. I googled, read a few scraping blogs and did some 1 on 1s. Finally, I just gave up and approach it a different way.

I will just have to scrape the headline.text from all 13 different links:

```
http://www.twittascope.com/?sign=aries
http://www.twittascope.com/?sign=gemini
http://www.twittascope.com/?sign=taurus
etc
```

by assigning a class variable to the homepage:

@@url = http://www.twittascope.com

With this variable, I was able to scrape for the 'tail' of the sublinks and just do this:

```
  doc = Nokogiri::HTML(open(@@url))
      main = doc.search("ul.site-sign-list li a").each do |t|
        url = @@url + t["href"]
```

This url method will return all the sublinks and then I will pass them through nokogiri once more to pull the headlines.

![](https://i.imgur.com/eZqZIgU.png)

So with this, instead of creating a names method, I created a headline method. I iterated the headlines with a .each_with_index to display:

```
1. Aries' Horoscope (Mar 21 - Apr 19)
2. Taurus' Horoscope (Apr 20 - May 20)
3. Gemini's Horoscope (May 21 - Jun 20)
4. Cancer's Horoscope (Jun 21 - Jul 22)
5. Leo's Horoscope (Jul 23 - Aug 22)
6. Virgo's Horoscope (Aug 23 - Sep 22)
```

I was ecstatic!

My next challenge would be to scrape yesterday's webpage and pull that horoscope.  I basically applied the same approach to yesterday and tomorrow's method.  But I have to execute nokogiri twice. 

```
def self.scrape_yesterday
    yesterdays = []
    scrape_urls.each do |site|
      title = Nokogiri::HTML(open(site))
        yesterday = title.search("ul.date-nav .yesterday").each do |yes|
          yesterday_url = "http://www.twittascope.com" + yes["href"]

          yes_doc = Nokogiri::HTML(open(yesterday_url))
          yes_copy = yes_doc.search(".dh-copy p").text
          yesterdays << yes_copy
        end
    end
    yesterdays
  end
	
	```
		
The first nokogiri scrapes the main link so that the second nokogiri can scrape the horoscope's yesterday link.

After all the scraping is done, I call those methods onto my CLI.  I realized, I don't need my horoscope.rb file.  I could just call my scraper methods onto my CLI.

```
def self.welcome
    Scraper.scrape_headline[0..12].each_with_index do |h1, index|
      puts "#{index+1}. #{h1}\n".colorize(:blue)
    end
  end
	```

After all the scraping and restructuring of my CLI, I double checked to make sure my def's are lining up with my ends.  Then I did the following housekeeping tasks of:

1) Even spacing -
    I didn't like how the options weren't spaced and how user's input would touch the next prompt.
	
2) Decorate it a little bit
    Some people used animations, I used the colorize gem to change the colors of return data.
		
3) Refactor

My own personal tidbit would be try to make the prompts sound more human.  

If you are reading this, I hope I've helped in some ways. Just know that you are not alone in this coding journey. Always reach out for help when you are stuck. You'll learn more, and faster.

In the meantime, check out my CLI and check your fortune!

Goodluck! 




