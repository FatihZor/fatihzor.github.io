---
layout: post
title:  "Named Gem Set"
date:   2015-08-01 15:22:15
categories:  [Ruby]
tags:  [Ruby]
---


## How could I install mutiple version of rails at my local?

[https://rvm.io/gemsets/basics](https://rvm.io/gemsets/basics "https://rvm.io/gemsets/basics")


RVM gives you compartmentalized independent ruby setups. This means that ruby, gems and irb are all separate and self-contained - from the system, and from each other.

You may even have separate named gemsets.

Let's say, for example, that you are testing two versions of a gem, with ruby 2.1.1. You can install one to the default 2.1.1, then create a named gemset for the other version, and switch between them easily.

**Example: testing gems**

	$ rvm 2.1.1@testing

will use a '2.1.1@testing' GEM_HOME (be sure to create it first), whereas:

	$ rvm 2.1.1

**Example: Rails versions & upgrading apps**

To illustrate the point, let's talk about a common use case. Assume you are testing out a rails application against a new Rails release. RVM makes such testing very easy, by letting you quickly switch between multiple Rails versions. First, let's set up the environments:

	$ rvm 2.1.1
	$ gem install rails -v 4.1.0
	
	$ rvm gemset create rails410 rails320
	Gemset 'rails410' created.
	Gemset 'rails320' created.
	
	$ rvm 2.1.1@rails410
	$ gem install rails -v 4.1.0
	
	$ rvm 2.1.1@rails320
	$ gem install rails -v 3.2.0

Note that, for each of the ruby installs above, you can have completely separate versions!

Now that your environments are set up, you can simply switch between Rails versions and Ruby versions as follows.

	$ rvm 2.1.1@rails410 ; rails --version

	Rails 4.1.0
	
	$ rvm 2.1.1@rails320 ; rails --version
	
	Rails 3.2.0

If you are deploying to a server, or you do not want to wait around for rdoc and ri to install for each gem, you can disable them for gem installs and updates. Just add the following line to your ~/.gemrc or /etc/gemrc:

	gem: --no-rdoc --no-ri