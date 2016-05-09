---
layout: post
title:  "Set up ROR development envrioment in Ubuntu"
date:   2015-07-28 22:22:15
categories:  [RoR]
tags:  [Rails]
---

All of the setups are in Ubuntu Linux


# - Install SSHD


install the ssh client and server with the following command:

`apt-get install openssh-client openssh-server`

edit the configuration file:

`cd /etc/ssh`

`vi sshd_config`

Disalbe Root Login:

`PermitRootLogin no`

Restart the service(under:/etc/ssh):

`service ssh restart`

So far the ssh is setup.
then we could ssh to the server on any server where ssh client is installed.

`ssh username@ip -p portNumber`

# - Install Apache

On Fedora, Apache is called "httpd",on ubuntu,it's called "apache2".
Apache is often pre-installed.

First let's check the Apache status by the following commands:

`service apache2 status`

if not installed,then nothing will show.

`apt-get install apache2`

check the status again, then you will see the service is running.


# - Install VSFTPD

- Very Secure FTP Server
- Replaces ftpd
- Easier than Scp
- Users can be locked in thier home directories

Install the application by the following command.

`apt-get install vsftpd`

`vi /etc/vsftpd.conf`

Do the follwing changes in the configuration file:

- Disable the annoymous access. 
	
		#Allow anonymous FTP?(Disable by default)
		annoymous_enable=NO

You could also set the ftpd_banner in the configuration file,and modify the welcome messages.

- enbale the writeable permission

		write_enable=YES

- Lock users in Home Directories

		chroot_local_user=YES

- Add one line

		allow_writeable_chroot=YES

you could also edit the configuration to and add the port of the ftp server:

	pasv_enable=YES
	pasv_min_port=65533
	pasv_max_port=65534
	pssv_address=127.0.0.1	


restart the services:

	service vsftpd restart
	
#### Testing vsftpd:

`cd /etc`

`ftp localhost`

then it will ask you to input the user name and password, you could use any linux username's account to go on.

list the files in the ftp server:

	ftp> ls
	
upload files:
	
	ftp> put welcome.txt
	ftp> ls
	
You could also use FileZilla GUI to test

# - Install Git

`apt-get install git`
`git --version`


# -Install SQLite,MySQL and potegreSQL

- install SQLite

	`apt-get install sqlite`
- install SQLite Tools

	`apt-get install sqlite3 libsqlite3-dev`
	
run the following commands to verify:	
	
	`sqlite3`
then input the following command to get help for sqlite.

	
	`.help`

- install MySQL

	`apt-get install mysql-server`
- verfiy the installation

	`service mysql status`
- start the client: 

	`mysql`
- set the password: 

	`UPDATE mysql.user SET Password=PASSWORD('zzz') WHERE User='root';`

	`mysql -h localhost -u root -p`

then it will ask for a password.
	
- install PostgreSQL

	`apt-get install postgresql postgresql-contrib`
	
- initialize a database

	`service postgresql initdb`
	
	`service postgresql start`
	
- connect to the database

	`su -postgres`
	
	`whoami`
	
	`psql`
	
		CREATE SCHEMA test;
		CREATE USER aaa PASSWORD 'yyy';
		CREATE ROLE
		GRANT ALL ON SCHEMA test TO aaa;
		GRANT ALL ON ALL TABLES IN SCHEMA test TO aaa;
		
		
	add user 'aaa' as a linux user:
	
	`addyser aaa`
	
	`su -aaa`
	
	`pssql -d postgres`
	
		CREATE TABLE test.test(coltest varchar(20));
		insert into test.test(coltest) values('it works');
		

# -Install Ruby and RVM

- install ruby

	`apt-get install ruby`

	`ruby -v`

- install RVM

	first remove ruby.

	`apt-get autoremove ruby`
	
	`\curl -L https://get.rvm.io | bash -s stable`
	
	RVM uses Linux users for access control;Add RVM users to the group rvm in the file `/etc/group`
		
		rvm:x:1002:jasper
		
- verify RVM

	`rvm install 1.9.3`,this will install the specified version.
	
	`rvm install ruby`,this will install the latest version.
	
	`rvm use 1.9.3`, this will switch to the version 1.9.3
	
	
	

# -Install Ruby on Rails

	gem install rails
	
	gem install sqlite3
	
	
testing Rails

	cd ~
	rails new blog
	cd blog
	ls
	rails server
	
	
	
	
