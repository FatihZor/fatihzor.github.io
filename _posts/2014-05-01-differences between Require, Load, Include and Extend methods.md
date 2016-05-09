---
layout: post
title:  "differences between Require, Load, Include and Extend methods"
date:   2014-05-01 15:22:15
categories:  [Ruby]
tags:  [Rails]
---


## differences between Require, Load, Include and Extend methods


## Include ##

When you Include a module into your class as shown below, it’s as if you took the code defined within the module and inserted it within the class, where you ‘include’ it. It allows the ‘mixin’ behavior. It’s used to DRY up your code to avoid duplication, for instance, if there were multiple classes that would need the same code within the module.
The following assumes that the module Log and class TestClass are defined in the same .rb file. If they were in separate files, then ‘load’ or ‘require’ must be used to let the class know about the module you’ve defined.


	module Log 
	  def class_type
	    "This class is of type: #{self.class}"
	  end
	end
	 
	class TestClass 
	  include Log 
	  # ... 
	end
	 
	tc = TestClass.new.class_type
	puts tc

The above will print “This class is of type: TestClass”

## Load ##

The load method is almost like the require method **except it doesn’t keep track of whether or not that library has been loaded**. So **it’s possible to load a library multiple times and also when using the load method you must specify the “.rb” extension of the library file name**.

Most of the time, you’ll want to use require instead of load but load is there if you want a library to be loaded each time load is called. For example, if your module changes its state frequently, you may want to use load to pick up those changes within classes loaded from.

Here’s an example of how to use load. Place the load method at the very top of your “.rb” file. Also the load method takes a path to the file as an argument:

	load 'test_library.rb'

So for example, if the module is defined in a separate .rb file than it’s used, then you can use the

`File: log.rb`

	module Log 
	  def class_type
	    "This class is of type: #{self.class}"
	  end
	end


 `File: test.rb`
	
	load 'log.rb'
	class TestClass 
	  include Log 
	  # ... 
	end
	

## Require ##

The require method allows you to load a library and prevents it from being loaded more than once. The require method will return ‘false’ if you try to load the same library after the first time. The require method only needs to be used if library you are loading is defined in a separate file, which is usually the case.

So it keeps track of whether that library was already loaded or not. You also don’t need to specify the “.rb” extension of the library file name.

Here’s an example of how to use require. Place the require method at the very top of your “.rb” file:

	require 'test_library'

## Extend ##

When using the extend method instead of include, you are adding the module’s methods as class methods instead of as instance methods.

Here is an example of how to use the extend method:

	module Log 
	  def class_type
	    "This class is of type: #{self.class}"
	  end
	end
	 
	class TestClass 
	  extend Log 
	  # ... 
	end
	 
	tc = TestClass.class_type
	puts tc

The above will print “This class is of type: TestClass”

When using extend instead of include within the class, if you try to instantiate TestClass and call method class_type on it, as you did in the Include example above, you’ll get a NoMethodError. So, again, the module’s methods become available as class methods.		


#File.expand_path

Converts a pathname to an absolute pathname. Relative paths are referenced from the current working **directory** of the **process** unless aDirString is given, in which case it will be used as the starting point. The given pathname may start with a ``~'', which expands to the process owner's home directory (the environment variable HOME must be set correctly). ``~ user'' expands to the named user's home directory.
	
	path-
		 |-Gemfile
		 |-to
			|-file.rb

in the file.rb file, if we want to get the path of GemFile we should use

	File.expand_path('../../Gemfile', __FILE__)

is a somewhat ugly Ruby idiom for getting the absolute path to a file when you know the path relative to the current file. Another way of writing it is this:

	File.expand_path('../Gemfile', File.dirname(__FILE__))

both are ugly, but the first variant is shorter. The first variant is, however, also very non-intuitive until you get the hang of it. Why the extra ..? (but the second variant may give a clue as to why it is needed).

This is how it works: File.expand_path returns the absolute path of the first argument, relative to the second argument (which defaults to the current working directory). __FILE__ is the path to the file the code is in. Since the second argument in this case is a path to a file, and File.expand_path assumes a directory, we have to stick an extra .. in the path to get the path right. This is how it works:

File.expand_path is basically implemented like this (in the following code path will have the value of ../../Gemfile and relative_to will have the value of /path/to/file.rb):

	def File.expand_path(path, relative_to=Dir.getwd)
	  # first the two arguments are concatenated, with the second argument first
	  absolute_path = File.join(relative_to, path)
	  while absolute_path.include?('..')
	    # remove the first occurrence of /<something>/..
	    absolute_path = absolute_path.sub(%r{/[^/]+/\.\.}, '')
	  end
	  absolute_path
	end
(there's a little bit more to it, it expands ~ to the home directory and so on -- there are probably also some other issues with the code above)

Stepping through a call to the code above absolute_path will first get the value /path/to/file.rb/../../Gemfile, then for each round in the loop the first .. will be removed, along with the path component before it. First /file.rb/.. is removed, then on the next round /to/.. is removed, and we get /path/Gemfile.

To make a long story short, File.expand_path('../../Gemfile', __FILE__) is a trick to get the absolute path of a file when you know the path relative to the current file. The extra .. in the relative path is to eliminate the name of the file in __FILE__.

#File.dirname

the absolute path of current file 

# Dir.pwd

current working directory

