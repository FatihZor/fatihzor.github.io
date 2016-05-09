---
layout: post
title:  "Configure Postgresql on ubuntu"
date:   2015-07-15 15:22:15
categories:  [Ruby]
tags:  [Ruby]
---


## Steps on configure postgresql on ubuntu


- Step 1: install the postgresql client and server

		sudo apt-get install postgresql-client		
		sudo apt-get install postgresql

- Step 2: install the postgresql GUI client:

		sudo apt-get install pgadmin3


- Step 3: adduser for postgresql

		sudo adduser dbuser
OR you could use the steps 7 to create the user.

		

- Step 4: switch to user postgres


		sudo su -postgres


- Step 5: 
		
		psql


- Step 6: Change the password for the user

	\password postgres

- Step 7: Create the dbuser with password

		
		CREATE USER dbuser WITH PASSWORD 'password';

- Step 8: Create database whose owner is dbuser:

		CREATE DATABASE exampledb OWNER dbuser;
		GRANT ALL PRIVILEGES ON DATABASE exampledb to dbuser;

- Step 9: quit
	
		\q