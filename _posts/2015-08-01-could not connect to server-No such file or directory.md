---
layout: post
title:  "could not connect to server: No such file or directory"
date:   2015-07-31 23:22:15
categories:  [Postgresql]
tags:  [Postgresql]
---


# Problem

When setting up the postgresql enviroment on the mac Yosemite, I run into such an issue:

	➜  ~  createuser test -P
	Enter password for new role:
	Enter it again:
	createuser: could not connect to database postgres: could not connect to server: 	No such file or directory
	Is the server running locally and accepting
	connections on Unix domain socket "/tmp/.s.PGSQL.5432"?

# Solution

- run `postgres -D /usr/local/var/postgres` to see more verbose message.

		➜  ~  postgres -D /usr/local/var/postgres
		LOG:  skipping missing configuration file "/usr/local/var/postgres/		postgresql.auto.conf"
		FATAL:  database files are incompatible with server
		DETAIL:  The data directory was initialized by PostgreSQL version 9.3, which 		is not compatible with this version 9.4.4.

- So I have to remove the previous data files and init again:
	
		rm -rf /usr/local/var/postgres && initdb /usr/local/var/postgres -E utf8
		
- at last,let make the postgresql start when the system starting.
	
		pg_ctl -D /usr/local/var/postgres -l logfile start

And then we could use the pgAdminIII GUI tool to connect to the postgresql server. By default, we could use the root user and password to login in Mac, of couse, we could go on creating a test user with:
		
		createuser test -P				
		Enter password for new role:
		Enter in again:
		
So far, Everything works fine.