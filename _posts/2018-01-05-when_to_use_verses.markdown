---
layout: post
title:      "when to use = verses =="
date:       2018-01-06 03:08:44 +0000
permalink:  when_to_use_verses
---

As I was working on the Ruby Music Library CLI lab, on the #list_songs_by_artist method, I was stuck and frustrated on the code that I have written and it was not passing the test.

This was my test requirement:

#list_songs_by_artist
    prompts the user to enter an artist
Please enter the name of an artist:
    accepts user input
    prints all songs by a particular artist in a numbered list (alphabetized by so
    does nothing if no matching artist is found

This was the code I had so far:

  **def list_songs_by_artist
    puts "Please enter the name of an artist:"
    input = gets.strip
    if artist == Artist.find_by_name(input)
      artist.songs.sort {|a, b| a.name <=> b.name}.each.with_index(1) do |song, index|
        puts "#{index}. #{song.name} - #{song.genre.name}"
      end
    end
  end**
	
	and this was the error I got:
	
	**Failures:
  1) CLI Methods #list_songs_by_artist prompts the user to enter an artist
     Failure/Error: if artist == Artist.find_by_name(input)
     NameError:
       undefined local variable or method `artist' for #<MusicLibraryController:0x
00000001abb1b0>**


artist was not defined.  I had mistakenly written the code by passing user's input into the Artist's find_by_name method thinking that if it matches the variable artist's name then it would carry out the following conditions.  My way of thinking is not logical in the way this method is supposed to carry out its functions.  

I took a sneak peak at the solutions and realized that my method could be solved by one simple fix.  Changing == to =.

I always thought you should be using the comparison == operator when writing conditions!

So I did 'Ask a Question' and after working with an instructor and Googling the term "Ruby one equal sign conditional", the instructor lead me to this page:

https://stackoverflow.com/questions/14567958/what-is-the-purpose-of-single-operator-equal-sign-in-ruby

So on the page:


**if foo = bar
end**

it can be read as this as well:

**foo = bar
if foo
 /do stuff/
end**

So this means the correct way to write my code is this:
**
    if artist = Artist.find_by_name(input)**
		
		which is the same as saying:
		
**		artist = Artist.find_by_name(input)
		if artist**
		
		
		So 'if artist' is true, then it will carry out the method, if not, then it won't do anything.
		
		So that's the different ways of using = and == when writing conditionals.
		
		
     
	
	
	


