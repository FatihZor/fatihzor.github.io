---
layout: post
title:  "Rake tasks step by step"
date:   2014-06-01 15:22:15
categories:  [Ruby]
tags:  [Rails]
---


## Rake tasks step by step

Rake tasks are placed in `lib/tasks` directory of application and files have .rake extension

### Simple Example ###

First, you must write a “Rakefile” file which contains the build rules. Here's a simple example:

	task :default => [:test]

	task :test do
	  ruby "test/unittest.rb"
	end

This Rakefile has two tasks:

- A task named “test”, which - upon invocation - will run a unit test file in Ruby.
- A task named “default”. This task does nothing by itself, but it has exactly one **dependency**, namely the “test” task. Invoking the “default” task will cause Rake to invoke the “test” task as well.

Running the “rake” command without any options will cause it to run the “default” task in the Rakefile:

	% ls
	Rakefile     test/
	% rake
	(in /home/some_user/Projects/rake)
	ruby test/unittest.rb
	....unit test output here...

### Simple greet rake task ###

	# lib/tasks/welcome.rake
	task :greet do
 	 puts “Hello !!”
	end

    ## Execute task
	rake greet

### Adding description to rake task ###

	# lib/tasks/welcome.rake
	desc “This is new style of greet”
	task :greet do
		puts “Hello !!”
	end

	## Execute task
	rake greet

### Adding namespace to rake tasks ###

It’s nothing but prefix that takes while executing rake task. Benefit of adding namespace is to categories similar rake tasks.

	 
	# lib/tasks/welcome.rake
	namespace :introduction do
	desc “This is one style of introduction”
	task :greet do
	  puts “Hello !!”
	end
	desc “This is 2nd style of introduction”
	task :hi do
	  puts “Hi ”
	end
	end

	## Execute task
	rake introduction:greet
	rake introduction:hi

### Passing arguments to rake tasks ###

	# lib/tasks/welcome.rake

	namespace :introduction do
	desc “This is one style of introduction”
	task :greet do
	  puts “Hello !!”
	end
	
	desc “This is 2nd style of introduction”
	task :hi => :enviroment do
	  puts “Hi #{ENV['name']}”
	end
	end


	## Execute task
	rake introduction:hi name=Raj

