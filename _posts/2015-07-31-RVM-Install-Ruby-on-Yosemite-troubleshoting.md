---
layout: post
title:  "issue fix when installing any ruby version on mac Yosemite"
date:   2015-07-31 23:22:15
categories:  [Asp.NET]
tags:  [RVM]
---


##  Problem:


Install other ruby via RVM, for example, I am trying to install the version 1.9.3 on mac, and the version of the Mac OS is Yosemite. I am always run into the issue:

`No binary rubies available for: osx/10.10/x86_64/ruby-1.9.3-p551`

Except that I am meeting a red error message telling me that
	
	Checking requirements for osx.
	Installing requirements for osx.
	Updating system.......
	Error running 'requirements_osx_brew_update_system ',
	please read /Users/HARSHA/.rvm/log/1380096954/update_system.log
	Requirements installation failed with status: 1.
	HARSHA:~ HARSHA$ rvm requirements
	Checking requirements for osx.
	Installing requirements for osx.
	Updating system.......
	Error running 'requirements_osx_brew_update_system ',
	please read /Users/HARSHA/.rvm/log/1380096969/update_system.log
	Requirements installation failed with status: 1.ystem.log
	Requirements installation failed with status: 1.
	
## Solution	

- `brew doctor`

	fix the issues the brew doctor tells you.

- Uninstall the current XCode,and download and reinstall the latest XCode.

- try `rvm install` again.

Everything works!





