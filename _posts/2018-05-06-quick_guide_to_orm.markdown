---
layout: post
title:      "Quick Guide to ORM"
date:       2018-05-07 01:41:29 +0000
permalink:  quick_guide_to_orm
---

Object Relational Mapping or ORM is exactly what its named.  To simplify things, it is how objects are related to each other.  A relationship as we understand it is a give and take process that makes it a full circle connection.  A user doesn't just receive comments about his posts, they also make comments on other people's post.

Here are a few tips when creating ORM databases.


A.	Draw it out on gliffy or create databases on DB Browser for SQLite

B. Create the primary key table first 
•	ex: User, Customer, CEO, the primary object

C. Then create secondary key table 
•	User makes Posts
•	Customer buy Brands
•	CEO pays Bills
•	The direct relationship object

D. Then there might be a few join tables
•	The Comments table
o	1. The comments they get from a post, through post_id
o	2. The comments they make on someone else’s post, through user_id
•	The Products table
o	1. The brands customer buys on Amazon, through brand_id
o	2. The brands customer sells on Amazon, through customer_id
•	The Vendors table
o	1. The bills a CEO pays is through the bills_id 
o	2. The bills a CEO bills other companies is through ceo_id
 	
* The important take-away is that not only are Users making comments, or Customers selling products, or that a CEO bills other companies, it is that these are reciprocal relationships. I may not have picked the right word for ‘Customer’ but I just want to explain the best that I can those relationships are reciprocal ones.  Which is why we need to alias to show the back and forth movement from each object of these relationships.

**Want to see if you did your alias associations correctly? **

-	go into your gem file
    o	add [gem ‘rails erd’]
-	go to your terminal
    o	run [bundle]
-	then run [rails erd]
-	open_erd.pdf
-	then a pdf file of the diagram will show




