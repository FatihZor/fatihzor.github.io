---
layout: post
title:  "RVM is not a function"
date:   2015-07-31 15:22:15
categories:  [Ruby]
tags:  [Ruby]
---


# rvm installation not working: “RVM is not a function” #

After run the command `\curl -sSL https://get.rvm.io | bash -s stable` in ubuntu, I thought the rvm is installed properly. unfortunately I run into the error `RVM is not a function`.

The solution to fix this issue is extremly easy:

You need to run the follow

	Jasper-PC$ source ~/.rvm/scripts/rvm
then run this

	Jasper-PC$ type rvm | head -n 1

and if you get

	rvm is a function

the problem is solved.

You also need to run 

	Jasper-PC$ rvm requirements 

to see dependency requirements for your operating system

Please Also Refer to :[https://rvm.io/integration/gnome-terminal](https://rvm.io/integration/gnome-terminal "https://rvm.io/integration/gnome-terminal") 