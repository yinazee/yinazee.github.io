---
layout: post
title:      "Key Concepts for Scraping"
date:       2018-01-04 18:57:03 -0500
permalink:  key_concepts_for_scraping
---

Scraping is a method to extract and reorganize data from HTML.  It breaks down information and puts them together again in a redefined API (application program interface). It is taking catered information from a variety of sources into your application.

Why Scraping? Scraping is a phenomenom when re-organized information can represent something new to a user.  Taking only information you need, simplifying and redefining the world into something new and more efficient. 

When using Scraping make sure to install gem Nokogiri by typing the following in your terminal:

gem install nokogirl

"Open-URI is a module in Ruby that allows us to programmatically make HTTP requests. It gives us a bunch of useful methods to make different types of requests, but for this guide, we're interested in only one: open.** This method takes one argument, a URL, and will return to us the HTML content of that URL.**" - From the Lesson

For example:

**html = open('http://www.google.com')**
*stores the HTML of Google into a variable called html. (More specifically, it actually stores the HTML in a temporary file that we can then call read on to get the raw HTML. 

On scraper.rb make sure you put:

1.	require 'nokogiri'
2.	require 'open-uri'

We can use the following line to grab the HTML that makes up the Flatiron School's landing page at flatironschool.com:

1.	html = open("https://flatironschool.com/")
*this will return the html code for that page

If the very text you need is **"350+ lives changed, and counting."**
Then be very specific with which css selector it lives in.
Open the element inspector, hover over the text you need and find the css selector that it is under.
In this case, it is under

1.	<span class="grey-text">...</span>

so how do you call the .css method? How do we use it?

In scraper.rb:

1.	require 'nokogiri'
2.	require 'open-uri'
3.	 
4.	doc = Nokogiri::HTML(open("http://flatironschool.com/"))

Let's call .css on doc and give it the argument of our CSS selector:


1.	require 'nokogiri'
2.	require 'open-uri'
3.	 
4.	doc = Nokogiri::HTML(open("http://flatironschool.com/"))
5.	**doc.css**(".grey-text")

If we puts out the result of that method call:
1.	puts doc.css(".grey-text")

We get:

1.	[#<Nokogiri::XML::Element:0x3ff8bdcc1a64 name="span" attributes=[#<Nokogiri::XML::Attr:0x3ff8bdcc19d8 name="class" value="grey-text">] children=[#<Nokogiri::XML::Text:0x3ff8bdcc12d0 "350+ lives changed,">, #<Nokogiri::XML::Element:0x3ff8bdcc11e0 name="br">, #


There's our text! Buried in there. To get it out, we can call .text on it:
1.	doc.css(".grey-text")**.text**
2.	 => "350+ lives changed,and counting."

# **Iterating over the elements**
Let's first get a list of the instructors from the flatironschool.com/teampage.

1.	require 'nokogiri'
2.	require 'open-uri'
3.	 
4.	html = open("https://web.archive.org/web/20160227204808/http://flatironschool.com/team")
5.	doc = Nokogiri::HTML(html)
6.	 
7.	instructors = doc.css("#instructors .team-holder .person-box")


Let's iterate over the instructors array with .each and puts out "Flatiron School <3 " followed by an instructor's name.

1.	instructors.each do |instructor| 
2.	  puts "Flatiron School <3 " + instructor.css("h2").text
3.	end

We'd see something like this:
1.	Flatiron School <3 Avi Flombaum
2.	Flatiron School <3 Joe Burgess



# **So, again when you begin scraping**

 FIRST STEP: set up some variables first:

1.	# This just opens a file and reads it into a variable
2.	html = File.read('fixtures/kickstarter.html')
3.	 
4.	kickstarter = Nokogiri::HTML(html)


solution to kickstarter scraping lab:

require "nokogiri"
require 'pry'

def create_project_hash
  html = File.read('fixtures/kickstarter.html')
  kickstarter = Nokogiri::HTML(html)
  projects = {}
  kickstarter.css("li.project.grid_4").each do |project|
    binding.pry

    title = project.css("h2.bbcard_name strong a").text
    projects[title] = {
      :image_link => project.css("div.project-thumbnail a img").attribute("src").value,
      :description => project.css("p.bbcard_blurb").text,
      :location => project.css("ul.project_meta span.location-name").text,
      :percent_funded => project.css("ul.project-stats li.first.funded strong").text.gsub("%", "").to_i
    }

end
projects
end

*do NOT put a space after location, put dash instead!
*one level down is a space
*class is represented by a period







