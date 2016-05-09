---
layout: post
title:  "Some tips for wget and cURL"
date:   2014-05-01 15:22:15
categories:  [Linux]
tags:  [Linux]
---

## wget ##

### basic usage ###

we always use wget to grab files from web servers,it is really useful tool for command line users. another tool also with the similar functionality is **cURL**.

- Anyway,the simplest way to use wget is as follows:

		$ wget http://myserver.com/path/to/file.txt

It simply connects to the http server on myserver.com and downloads the file file.txt

- But what will happen if the connection is slow, and the file is lengthy? The connection will probably fail before the whole file is retrieved, more than once. In this case, Wget will try getting the file until it either gets the whole of it, or exceeds the default number of retries (this being 20). It is easy to change the number of tries to 45, to insure that the whole file will arrive safely:

		wget --tries=45 http://fly.cc.fer.hr/jpg/flyweb.jpg

- Now let's leave Wget to work in the background, and write its progress to log file `log'. It is tiring to type `--tries', so we shall use `-t'.


		wget -t 45 -o log http://fly.cc.fer.hr/jpg/flyweb.jpg &


- The usage of FTP is as simple. Wget will take care of login and password.


		$ wget ftp://gnjilux.cc.fer.hr/welcome.msg
		--23:35:55--  ftp://gnjilux.cc.fer.hr:21/welcome.msg
		           => `welcome.msg'
		Connecting to gnjilux.cc.fer.hr:21... connected!
		Logging in as anonymous ... Logged in!
		==> TYPE I ... done.  ==> CWD not needed.
		==> PORT ... done.    ==> RETR welcome.msg ... done.
		Length: 1,340 (unauthoritative)
		 
		0K -> .
 
		23:35:56 (37.39K/s) - `welcome.msg' saved [1340]

- If you specify a directory, Wget will retrieve the directory listing, parse it and convert it to HTML. Try:
	 	wget ftp://prep.ai.mit.edu/pub/gnu/
		lynx index.html

- Most people using wget thought will be using it to grab large or many files. Useful parameters for this are -c option (for continue) which will actually allow a ‘broken’ connection and continue downloading the file when the connection resumes (handy if grabbing large files over  a flakey connection):

		$ wget -c http://myserver.com/path/to/big.iso

### Advanced Usage ###

- Regex/wildcards

You want to download all the GIFs from an HTTP directory. `wget http://host/dir/*.gif' doesn't work, since HTTP retrieval does not support globbing. In that case, use:

	wget -r -l1 --no-parent -A.gif http://host/dir/

It is a bit of a kludge, but it works. `-r -l1' means to retrieve recursively (See section Recursive Retrieval), with maximum depth of 1. `--no-parent' means that references to the parent directory are ignored (See section Directory-Based Limits), and `-A.gif' means to download only the GIF files. `-A "*.gif"' would have worked too.



Basically, wget doesn’t allow the standard CLI wildcards such as * or ? etc. 
Let's say we want to download 3 images from a server folder, then you could do it as following:

		wget http://myserver.com/path/images/{A.jpg,B.png,C.gif}
		
	OR use the following command, it will reculcively download the structrue:
		
		wget -r -l1 -A "*.jpg" -A "*.png"  http://myserver.com/path/images/
	Or

		wget -r -l1 -A.jpg -A.png http://myserver.com/path/images/


- if you want to encode your own username and password to HTTP or FTP, use the appropriate URL syntax (See section URL Format).


		wget ftp://username:mypassword@jagor.srce.hr/.emacs


#cURL

	
[http://curl.haxx.se/docs/manual.html](http://curl.haxx.se/docs/manual.html "http://curl.haxx.se/docs/manual.html")
