git-download-mantis
=========

Ansible role that downloads and installs a chosen release of the Mantis Bug Tracking software to the default document root for the Apache webserver.

Requirements
------------

Need to have a Debian based Linux (Ubuntu, Debian, etc.) setup with MySQL and Apache already setup and configured. This role uses the default `/var/www/html` document root path to install the Mantis BT software.

Role Variables
--------------

Choose the git tagged release that you would like to download and install. Comment this out if using a git branch instead.
```
	tagged_release_version: "release-2.15.0"
```
The git repo for the Mantis Bug Tracker (BT). This is the default but can be changed if you have a forked/modified git repo that you would prefer to use.
```
	git_repo: "https://github.com/mantisbt/mantisbt.git"
```
The DB user the application will use to connect. The default is 'mantisdbuser'. 
```
	db_username: 'mantisdbuser'
``` 
The DB password used by the db_username value to connect to the database. The default is an empty string.

```
	db_password: ''
```
The name of the database to create and use for Mantis BT. The default is 'bugtracker'
```
	database_name: 'bugtracker'
```
The Document Root or file path where Mantis files will be stored and served up by your webserver. The default path is "/var/www/html" and assumes you are running Apache2 on Debian or Ubuntu
```
	web_files_path: "/var/www/html"
```
The linux username used by your webserver. The default value is "www-data" which assumes Apache is used on a Debian or Ubuntu linux
```
	web_user: "www-data"
```
The linux group used by your webserver. The default value is "www-data" which assumes Apache is used on a Debian or Ubuntu linux
```
	web_group: "www-data"
```

Dependencies
------------

	- stancel.apache-webserver

Example Playbook
----------------

	- hosts: your_new_mantis_server
	  vars_files:
	    - vars/main.yml
	  roles:
	    - { role: stancel.git-download-mantis }


or 


	- hosts: your_new_mantis_server 
	  vars:
		tagged_release_version: "release-2.15.0"
	  roles:
	    - { role: stancel.git-download-mantis }

License
-------

GPLv3

Author Information
------------------

Brad Stancel
