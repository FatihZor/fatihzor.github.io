---
layout: post
title:  "why bundle exec rake db:migrate"
date:   2015-08-01 15:22:15
categories:  [Ruby]
tags:  [Ruby]
---


## what dose `bundle exec rake db:migrate` mean?



 It's very simple. bundle exec is a Bundler command to execute a script in the context of the current bundle (the one from your directory's Gemfile). `rake db:migrate` is the script where db is the namespace and migrate is the task name defined.

So bundle exec rake db:migrate executes the rake script with the command db:migrate in the context of the current bundle.

As to the "why?" I'll quote from the bundler page:

> In some cases, running executables without bundle exec may work, if the executable happens to be installed in your system and does not pull in any gems that conflict with your bundle.
> 
> However, this is unreliable and is the source of considerable pain. Even if it looks like it works, it may not work in the future or on another machine.



Here's an example Gemfile:

	source 'http://rubygems.org'

	gem 'rails', '2.8.3'
	gem 'rack',  '~> 1.1.0'
	gem 'rake', '~> 0.9.2.2'
	Here, bundle exec would execute the script using rack version 1.1.0 and rake version 0.9.2.2.

Here, `bundle exec` would execute the script using rack version 1.1.0 and rake version 0.9.2.2.

More information about the tool bundle, please refer to [http://bundler.io/](http://bundler.io "http://bundler.io")