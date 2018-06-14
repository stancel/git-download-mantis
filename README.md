git-download-mantis
=========

Ansible role that downloads and installs a chosen release of the Mantis Bug Tracking software to the default document root for the Apache webserver.

Requirements
------------

Need to have a Debian based Linux (Ubuntu, Debian, etc.) setup with MySQL and Apache already setup and configured. This role uses the default `/var/www/html` document root path to install the Mantis BT software.

Role Variables
--------------

Choose the git tagged release that you would like to download and install

	`tagged_release_version: "release-2.15.0"`

The git repo for the Mantis Bug Tracker (BT). This is the default but can be changed if you have a forked/modified git repo that you would prefer to use.

	`git_repo: "https://github.com/mantisbt/mantisbt.git"``


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
