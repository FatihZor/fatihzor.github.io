---
layout: post
title:  "Ruby singleton-class definitions"
date:   2014-06-01 15:22:15
categories:  [Ruby]
tags:  [Rails]
---


## Ruby singleton class definitions

Examples:
	
	class << obj
		  def test
		     :
		  end
		     :
	end

Syntax:

	class `<<' expr
	  expr..
	end

Defines the class attribute for certain object. The definitions within this syntax only affect the specified object.

But people more commonly use this feature for syntactic gymnastics like this:

	class Thing
	  def do_something
	  end
	
	  class << self
	    def foo
	      puts "I am #{self}"
	    end
	  end
	end

Or

	class Thing
	  def do_something
	  end
	
	  class << Thing
	    def foo
	      puts "I am #{self}"
	    end
	  end
	end

When this code -- this class definition -- executes, what is self? It's the class Thing. Which means class << self is the same as saying "add the following methods to class Thing." That is, foo is a class method. After the above completes, you can do this:

	t = Thing.new
	t.do_something  => does something
	t.class.foo     => "I am Thing"
	t.foo           => NoMethodError: undefined method `foo'

And when you think about what << is doing, it all makes sense. It's a way to append to a particular instance, and in the common case, the instance being appended to is a class, so the methods within the block become class methods.

In short, it's a terse way to create class methods within a class definition block. Another way would be to do this:

	class Thing
	  def self.foo
	    # ...
	  end
	end

Same thing. Your example is actually a syntax error, but if you understand how << is used with instances and the class keyword, you'll know how to correct it.