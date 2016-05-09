---
layout: post
title:  "why bundle exec rake db:migrate"
date:   2014-07-01 15:22:15
categories:  [Ruby]
tags:  [Ruby]
---


## Some Ruby Idioms


- Methods such as empty! and empty?

Ruby method names can end with an exclamation mark (a bang method)
or a question mark (a predicate method). Bang methods normally do
something destructive to the receiver. Predicate methods return true or
false depending on some condition.

- a || b

The expression a || b evaluates a. If it isn ’t false or nil, then evaluation stops,
and the expression returns a. Otherwise, the statement returns b. This is a
common way of returning a default value if the first value hasn ’t been set.

- a ||= b

The assignment statement supports a set of shortcuts: a op= b is the same
as a = a op b. This works for most operators.

	count += 1 # same as count = count + 1
	price *= discount # price = price * discount
	count ||= 0 # count = count || 0

So, count ||= 0 gives count the value 0 if count doesn ’t already have a value.



- obj = self.new

Sometimes a class method needs to create an instance of that class.

	class Person < ActiveRecord::Base
		def self.for_dave
			Person.new(name: 'Dave' )
		end
	end

This works fine, returning a new Person object. But later, someone might
subclass our class.

	class Employee < Person
		# ..
	end
	dave = Employee.for_dave # returns a Person

The `for_dave()` method was hardwired to return a Person object, so that’s
what is returned by Employee.for_dave. Using self.new instead returns a new
object of the receiver’s class, Employee.

- lambda

The lambda operator converts a block into an object of type Proc. An alternate
syntax, introduced in Ruby 1.9, is ->.


- require File.expand_path('../../config/environment', __FILE__)


 Ruby’s require method loads an external source file into our application.
This is used to include library code and classes that our application relies
on. In normal use, Ruby finds these files by searching in a list of directories, the LOAD_PATH.

Sometimes we need to be specific about what file to include. We can do
that by giving require a full filesystem path. The problem is, we don ’t know
what that path will be —our users could install our code anywhere.

Wherever our application ends up getting installed, the relative path
between the file doing the requiring and the target file will be the same.
Knowing this, we can construct the absolute path to the target by using
the File.expand_path() method, passing in the relative path to the target file,
as well as the absolute path to the file doing the requiring (available in
the special variable __FILE__).

In addition, there are many good resources on the Web showing Ruby idioms
and Ruby gotchas. Here are just a few:


1.  http://www.ruby-lang.org/en/documentation/ruby-from-other-languages/
1.  http://en.wikipedia.org/wiki/Ruby_programming_language
1.  http://www.zenspider.com/Languages/Ruby/QuickRef.html