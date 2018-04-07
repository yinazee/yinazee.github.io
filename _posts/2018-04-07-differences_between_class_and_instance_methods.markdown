---
layout: post
title:      "Differences Between Class and Instance Methods"
date:       2018-04-07 16:14:57 -0400
permalink:  differences_between_class_and_instance_methods
---


Albert Einstein said, "If you can't explain it simply, then you don't understand it well enough."

Okay, so here we go.

Inorder to understand the concept better, let's find a real life analogy to help explain the differences between Class and Instance Methods.

# Class Method

For example: 

Let's use a Dog **class** and give it a bark **class method** and a owners **instance method**.  This is what they look like:

```
class Dog

def self.bark
  puts "Woof!"
end

def owner
  puts "Mary"
end


end
```

A class method is the call of a function onto the object Dog **itself**.  So whenever you want to invoke a **class method**, it MUST be on a **class object**.  You can simply add '.self' in front of the method name to create this function. Self refers to the object itself.

```

self.bark = Dog.bark

Dog.bark

#=> Woof!

```


# Instance Method
For example:


```
class Dog

def self.bark
  puts "Woof!"
end

def owner
  puts "Mary"
end


end
```

In this Dog class example, you can't just command:

```
Dog.owner

#=> NoMethodError: undefined method ‘owner'
```


The class itself can't access instance methods.  

Instance methods are what makes each class different from one another. A dog class may have an owner method but a company class may have an employees method, a couch class may have a materials method, etc.  Every class have their own instance methods.

So how do we invoke instance methods? How do we use them?

Let's create a dog and save it to a variable.


```
lassie = Dog.new
```

So the Dog class machine just churned out a new **instance** of a dog, and we set it to variable 'lassie'.  And just like class methods, only instance methods can be called on instance objects.

So taking from what we have so far....

```
class Dog

def self.bark
  puts "Woof!"
end

def owner
  puts "Mary"
	*or write a method that will find the dog's owner.
end


end
```

We can now call the **owner instance method** on the **lassie instance object**.

```
lassie.owner = Mary
```


# Class Methods vs. Instance Methods

When creating objects, be aware of how these objects and data are accessed, as class methods are accessed by invoking directly on the class itself verses instance methods that are only accessed on the instance objects of that class.

sources:
http://www.culttt.com/2015/06/10/understanding-class-methods-verses-instance-methods-in-ruby/
http://www.railstips.org/blog/archives/2009/05/11/class-and-instance-methods-in-ruby/
https://www.youtube.com/watch?time_continue=449&v=ab11lJJKm8M

