git-download-mantis
=========

Ansible role that downloads and installs a chosen release of the Mantis Bug Tracking software to the default document root for the Apache webserver. When pulling up the URL of your Mantis installation after this role has been run you should see the installation screens that will check the requirements and install the database (DDL) scripts. Once that is completed you should login with the following info:  

```
	username: administrator
	password: root
```
After that you should remove the `<install_path>/admin` folder

Requirements
------------

Need to already have MySQL / MariaDB / Percona Server and your webserver (Apache or Nginx) already setup and configured. The defaults assume a Debian based Linux (Ubuntu, Debian, etc.) with a default webserver document root of `/var/www/html` to install the Mantis BT software. You can override those default variables if that is not the case.

Role Variables
--------------

Choose the git tagged release that you would like to download and install. Comment this out if using a git branch instead.  

```
	git_download_mantis_tagged_release_version: "release-2.18.0"
```
The git repo for the Mantis Bug Tracker (BT). This is the default but can be changed if you have a forked/modified git repo that you would prefer to use.  

```
	git_download_mantis_git_repo: "https://github.com/mantisbt/mantisbt.git"
```
The database to create when setting up the application. The default is `bugtracker`.  

```
	git_download_mantis_db_name: 'bugtracker'
```
The DB user the application will use to connect. The default is `mantisWebUser`.   

```
	git_download_mantis_db_username: 'mantisWebUser'
``` 
The password for the DB user being created. No default value set.

```
	git_download_mantis_db_password: "some-really-secure-password"
```
The root password for your MySQL, MariaDB or Percona Server DB instance to create the DB and user.

```
	git_download_mantis_mysql_root_password: "your MySQL root password"
```
The Document Root or file path where Mantis files will be stored and served up by your webserver. The default path is "/var/www/html" and assumes you are running Apache2 on Debian or Ubuntu.  

First part => *git_download_mantis_web_files_path:* is the root directory of your webserver

Second part =>  git_download_mantis_*web_directory_for_application:* is the application directory inside the root directory

!Be aware of the starting / !

```
    git_download_mantis_web_files_path: "/var/www"
    git_download_mantis_web_directory_for_application: "/html"
```
The linux username used by your webserver. The default value is `www-data` which assumes Apache is used on a Debian or Ubuntu linux.  

```
	git_download_mantis_web_user: "www-data"
```
The linux group used by your webserver. The default value is `www-data` which assumes Apache is used on a Debian or Ubuntu linux.  

```
	git_download_mantis_web_group: "www-data"
```
Manage package with apt, you can disable the installation of package
```
	git_download_mantis_manage_packages: true
```

The php.ini configurations, to allow or not the setting of these items, useful if your server is already setup with different values, default are true```
```
	git_download_mantis_configure_mysqli_allow_local_infile: true
	git_download_mantis_configure_memory_limit: true
	git_download_mantis_configure_post_max_size: true
	git_download_mantis_configure_upload_max_filesize: true
	git_download_mantis_configure_max_input_time: true
	git_download_mantis_configure_max_execution_time: true
	git_download_mantis_configure_php_timezone: true
```

Install Composer or not, default is true, disable it if you already have composer installed
```
	git_download_mantis_install_composer: true
```

Is this a "new", "upgrade" or "restore" installation? "new" and "upgrade" installs install files from Git, "restore" skips any git deployments and expect a later role to restore files to the needed directory. Default is "new".
```
	git_download_mantis_installation_type: "new"
```

Is this instance to be used for a "dev", "qa" or "prod" environment? Only "prod" environments will deploy the SuiteCRM schedulers. Default is "prod".
```
	git_download_mantis_environment_type: "prod"
```


Dependencies
------------

	None

Example Playbook
----------------

	- hosts: your_new_mantis_server
	  vars_files:
	    - vars/main.yml
	  roles:
	    - stancel.git-download-mantis


or 


	- hosts: your_new_mantis_server 
	  vars:
		git_download_mantis_tagged_release_version: "release-2.18.0"
	  roles:
	    - stancel.git-download-mantis

License
-------

GPLv3

Author Information
------------------

[Brad Stancel](https://github.com/stancel) 


