Title:  OpenShift Enterprise Summit - Lab Manual
Author: Grant Shipley  
Date:   May, 2013

#**Contents**#

1. **Overview of OpenShift Enterprise**
2. **Installing OpenShift Enterprise**
3. **Installing the RHC client tools**
4. **Using *rhc setup***
5. **Creating a PHP application**
6. **Scaling an application**
7. **Java EE applications using JBoss EAP**


#**Lab 1: Overview of OpenShift Enterprise**

#**1.0 Overview of OpenShift Enterprise**

##**1.1 Assumptions**
This lab manual assumes that you are attending the Red Hat Summit Lab Session and that you will be using this lab manual in conjunction with the workshop.  

It is also assumed that you have been granted access to two Red Hat Enterprise Linux servers with which to perform the exercises in this lab manual.  If you do not have access to your servers, please notify the session leaders.

 A working knowledge of SSH, git, and yum, and familiarity with a Linux-based text editor are assumed.  If you do not have an understanding of any of these technologies, please let the session leaders know.

##**1.2 What you can expect to learn from this lab**

At the conclusion of this class, you should have a solid understanding of how to install and configure OpenShift Enterprise.  You should also feel comfortable in the usage of creating and deploying applications using the OpenShift Enterprise web console, and command line tools.

##**1.3 Overview of OpenShift Enterprise PaaS**

Platform as a Service is changing the way developers approach developing software. Developers typically use a local sandbox with their preferred application server and only deploy locally on that instance. Developers typically start JBoss locally using the startup.sh command and drop their .war or .ear file in the deployment directory and they are done.  Developers have a hard time understanding why deploying to the production infrastructure is such a time consuming process.

System Administrators understand the complexity of not only deploying the code, but procuring, provisioning and maintaining a production level system. They need to stay up to date on the latest security patches and errata, ensure the firewall is properly configured, maintain a consistent and reliable backup and restore plan, monitor the application and servers for CPU load, disk IO, HTTP requests, etc.

OpenShift Enterprise provides developers and IT organizations an auto-scaling cloud application platform for quickly deploying new applications on secure and scalable resources with minimal configuration and management headaches. This means increased developer productivity and a faster pace in which IT can support innovation.

This manual will walk you through the process of installing and configuring an OpenShift Enterprise environment as part of this workshop that you are attending.

##**1.4 Overview of IaaS**

The great thing about OpenShift Enterprise is that we are infrastructure agnostic. You can run OpenShift on bare metal, virtualized instances, or on public/private cloud instances. The only thing that is required is Red Hat Enterprise Linux as the underlying operating system. We require this in order to take advantage of SELinux and other enterprise features so that you can ensure your installation is rock solid and secure.

What does this mean? This means that in order to take advantage of OpenShift Enterprise, you can use any existing resources that you have in your hardware pool today. It doesn’t matter if your infrastructure is based on EC2, VMware, RHEV, Rackspace, OpenStack, CloudStack, or even bare metal as we run on top of any Red Hat Enterprise Linux operating system as long as the architecture is x86_64.

<!--BREAK-->

#**Lab 2: Installing OpenShift Enterprise**

**Server used:**

* broker host
* node host

**Tools used:**

* TBD

CONTENT TBD 

<!--BREAK-->

#**Lab 3: Installing the RHC client tools**

**Server used:**

* localhost

**Tools used:**

* ruby
* sudo
* git
* yum
* gem
* rhc

The OpenShift Client tools, known as **rhc**, are built and packaged using the Ruby programming language.  OpenShift Enterprise integrates with the Git version control system to provide powerful, decentralized version control for your application source code.

OpenShift Enterprise client tools can be installed on any operating system with Ruby 1.8.7 or higher.  Instructions for specific operating systems are provided below. It is assumed that you are running the commands from a command line window, such as Command Prompt, or Terminal. If you are using Ruby Version Manager (rvm) see the instructions below.

##**Microsoft Windows**

###**Installing Ruby for Windows**

[RubyInstaller 1.9](http://rubyinstaller.org/) provides the best experience for installing Ruby on Windows XP, Vista, and Windows 7. Download the newest version from the [download page](http://rubyinstaller.org/downloads/) and launch the installer.

**Important**: During the installation you should accept all of the defaults, it is mandatory that you select the "Add Ruby executables to your PATH" check box in order to run Ruby from the command line.

After the installation is complete, to verify that the installation is working run:
	
	C:\Program Files\> ruby -e 'puts "Welcome to Ruby"'
	Welcome to Ruby

If the 'Welcome to Ruby' message does not display, the Ruby executable may not have been added to the path. Restart the installation process and ensure the "Add Ruby executables to your PATH" check box is selected.

###**Installing Git for Windows**

The next step is to install [Git for Windows](http://msysgit.github.com/) so that you can synchronize your local application source and your OpenShift application. Git for Windows offers the easiest Git experience on the Windows operating system and is the recommended default - if you use another version of Git please ensure it can be executed from the command line and continue to the next section.

Download and install the [latest version of Git for Windows](http://code.google.com/p/msysgit/downloads/list?q=full+installer+official+git). Ensure that Git is added to your PATH so that it can be run from the command line. After the installation has completed, verify that Git is correctly configured by runing:

	C:\Program Files\> git --version
	git version 1.7.11.msysgit.1

###**Installing RHC for Windows**

After Ruby and Git are correctly installed, use the RubyGems package manager (included in Ruby) to install the OpenShift Enterprise client tools. Run:

	C:\Program Files\> gem install rhc

RubyGems downloads and installs the rhc gem from www.rubygems.org/gems/rhc. The installation typically proceeds without errors. After the installation has completed, run:

	C:\Program Files\> rhc

##**Mac OS X**

###**Installing Ruby for OS X**

From OS X Lion onwards, Ruby 1.8.7 is installed by default. On older Mac systems, Ruby is shipped as part of the [Xcode development suite](https://developer.apple.com/xcode/) and can be installed from your installation CD. If you are familiar with Mac development, you can also use [MacRuby](http://macruby.org/) or see the Ruby installation page for [help installing with homebrew](http://www.ruby-lang.org/en/downloads/).

To verify that Ruby is correctly installed run:

	$ ruby -e 'puts "Welcome to Ruby"'
	Welcome to Ruby
	
###**Installing Git for OS X**

There are a number of options on Mac OS X for Git. We recommend the Git for OS X installer - download and run the latest version of the dmg file on your system. To verify the [Git for OS X installation](http://code.google.com/p/git-osx-installer/), run:

	$ git --version
	git version 1.7.11.1

###**Installing RHC for OS X**

With Ruby and Git installed, use the RubyGems library system to install and run the OpenShift Enterprise gem. Run:

	$ sudo gem install rhc

After the installation has completed, run:

	$ rhc -v

##**Fedora 16, 17, and 18**

To install from yum on Fedora 16, 17, or 18, run:

	$ sudo yum install rubygem-rhc

This installs Ruby, Git, and the other dependencies required to run the OpenShift Enterprise client tools.

After the OpenShift Enterprise client tools have been installed, run:

	$ rhc -v

##**Red Hat Enterprise Linux 6.2, 6.3 or 6.4**

The most recent version of the OpenShift Enterprise client tools are available as a RPM from the OpenShift Enterprise hosted YUM repository. We recommend this version to remain up to date, although a version of the OpenShift Enterprise client tools RPM is also available through EPEL.

To add the OpenShift Enterprise YUM repository, download the repository file openshift.repo and move it to your **/etc/yum.repos.d/** directory.

	$ sudo mv ~/openshift.repo /etc/yum.repos.d/

In order to install the rubygems package, the *RHEL Optional* channel must be enabled. There are two ways of doing this from the command line.  If you are using the Certificate-Based RHN tooling, enter the following command:

	$ sudo yum-config-manager --enable rhel-6-server-optional-rpms   

If you are using RHN-Classic, enter the following command:

	$ sudo rhn-channel --add --channel=rhel-x86rhel-x86_64-server-optional-6

With the repository in place, you can now install the OpenShift Enterprise client tools by running the following command:

	$ sudo yum install rubygem-rhc

##**Ubuntu**

Use the apt-get command line package manager to install Ruby and Git before you install the OpenShift Enterprise command line tools. Run:

	$ sudo apt-get install ruby-full rubygems git-core

After you install both Ruby and Git, verify they can be accessed via the command line:

	$ ruby -e 'puts "Welcome to Ruby"'
	$ git --version

If either program is not available from the command line, please add them to your PATH environment variable.

With Ruby and Git correctly installed, you can now use the RubyGems package manager to install the OpenShift Enterprise client tools. From a command line, run:

	$ sudo gem install rhc


**Lab 3 Complete!**

<!--BREAK-->

#**Lab 4: Using *rhc setup***

**Server used:**

* localhost

**Tools used:**

* rhc

##**Configuring RHC setup**

By default, the RHC command line tool will default to use the publicly hosted OpenShift environment.  Since we are using our own enterprise environment, we need to tell *rhc* to use our broker.example.com server instead of openshift.com.  In order to accomplish this, run the *rhc setup* command:

	$ rhc setup —server broker.example.com
	
Once you enter in that command, you will be prompted for the username that you would like to authenticate with.  For this workshop, use the *demo* user account that we created in a previous lab.  After providing the username that you would like to connect with, you will be prompted for the password of the user account.

The next step in the setup process is to create and upload our SSH key to the broker server.  This is required for pushing your source code, via git, up to the OpenShift Enterprise server.

Finally, you will be asked to create a namespace for the provided user account.  The namespace is a unique name which becomes part of your application URL. It is also commonly referred to as the users domain. The namespace can be at most 16 characters long and can only contain alphanumeric characters. There is currently a 1:1 relationship between usernames and namespaces.  For this lab, create the following namespace:

	ose

##**Under the covers**

The *rhc setup* tool is a convenient command line utility to ensure that the user’s operating system is configured properly to create and manage applications from the command line.  After this command has been executed, a *.openshift* directory was created in the users home directory with some basic configuration items specified in the *express.conf* file.  The contents of that file are as follows:

	# Default user login
	default_rhlogin=‘demo’

	# Server API
	libra_server = 'broker.example.com'
	
This information will be provided to the *rhc* command line tool for every future command that is issued.  If you want to run commands as a different user than the one listed above, you can either change the default login in this file or provide the *-l* switch to the *rhc* command.


**Lab 4 Complete!**

<!--BREAK-->
#**Lab 5: Creating a PHP application**

**Server used:**

* localhost
* node host

**Tools used:**

* rhc

In this lab, we are ready to start using OpenShift Enterprise to create our first application.  To create an application, we will be using the *rhc app* command.  In order to view all of the swtiches available for the *rhc app* command, enter the following command:

	$ rhc app -h
	
This will provide you with the following output:

	List of Actions
 	create             Create an application and adds it to a domain
  	git-clone          Clone and configure an application's repository locally
  	delete             Delete an application from the server
  	start              Start the application
  	stop               Stop the application
  	force-stop         Stops all application processes
  	restart            Restart the application
  	reload             Reload the application's configuration
  	tidy               Clean out the application's logs and tmp directories and tidy up the git repo on the server
  	show               Show information about an application
  	status             Show status of an application's gears

	Global Options
  	-l, --rhlogin login       OpenShift login
  	-p, --password password   OpenShift password
  	-d, --debug               Turn on debugging
  	--timeout seconds         Set the timeout in seconds for network commands
  	--noprompt                Suppress the interactive setup wizard from running before a command
  	--config FILE             Path of a different config file
  	-h, --help                Display help documentation
  	-v, --version             Display version information


##**Create a new application**

It is very easy to create an OpenShift Enterprise application using *rhc*. The command to create an application is *rhc app create* and it requires two mandatory arguments:

* **Application Name (-a or --app)** : The name of the application. The application name can only contain alpha-numeric characters and at max contain only 32 characters.

* **Type (-t or --type)**: The type is used to specify which language runtime to use.  

Create a directory to hold your OpenShift Enterprise code projects:

	$ cd ~
	$ mkdir ose
	$ cd ose
	
To create an application that uses the *php* runtime, issue the following command:

	$ rhc app create -a firstphp -t php
	
After entering that command, you should see the following output:


	Password: ****
	
	Creating application 'firstphp'
	===============================
	
	  Namespace: ose
	  Scaling:   no
	  Cartridge: php
	  Gear Size: default
	
	Your application's domain name is being propagated worldwide (this might take a minute)...
	The authenticity of host 'firstphp-ose.example.com (10.4.59.221)' can't be established.
	RSA key fingerprint is 6c:a5:e5:fa:75:db:5a:7f:dc:a2:44:ed:e4:97:af:3c.
	Are you sure you want to continue connecting (yes/no)? yes
	Cloning into 'firstphp'...
	done
	
	firstphp @ http://firstphp-ose.example.com/
	===========================================
	  Application Info
	  ================
	    Git URL   = ssh://e9e92282a16b49e7b78d69822ac53e1d@firstphp-ose.example.com/~/git/firstphp.git/
	    UUID      = e9e92282a16b49e7b78d69822ac53e1d
	    Created   = 1:47 PM
	    Gear Size = small
	    SSH URL   = ssh://e9e92282a16b49e7b78d69822ac53e1d@firstphp-ose.example.com
	  Cartridges
	  ==========
	    php-5.3
	
	RESULT:
	Application firstphp was created.
	


If you completed all of the steps in lab 16 correctly, you should be able to verify that your application was created correctly by opening up a web browser and entering the following URL:

	http://firstphp-ose.example.com
	
You should see the default template that OpenShift Enterprise uses for a new application.

![](http://training.runcloudrun.com/images/firstphp.png)

##**What just happened?**

After you entered the command to create a new PHP application, a lot of things happened under the covers:

* A request was made to the broker application host to create a new php application
* A message was dropped using MCollective and ActiveMQ to find a node host to handle the application creation request
* A node host responded to the request and created an application / gear for you
* All SELinux and cgroup policies were enabled for your application gear
* A userid was created for your application gear
* A private git repository was created for your gear on the node host
* The git repository was cloned on your local machine
* BIND was updated on the broker host to include an entry for your application

##**Understanding the directory structure on the node host**
	
It is important to understand the directory structure of each OpenShift Enterprise application gear.  For the PHP application that we just created, we can verify and examine the layout of the gear on the node host.  SSH to your node host and execute the following commands:

	# cd /var/lib/openshift
	# ls
	
You will see output similar to the following:

	e9e92282a16b49e7b78d69822ac53e1d
	
The above is the unique user id that was created for your application gear.  Lets examine the contents of this gear by using the following commands:

	# cd e9e92282a16b49e7b78d69822ac53e1d
	# ls -al
	
You should see the following directories:

	total 44
	drwxr-x---.  9 root e9e92282a16b49e7b78d69822ac53e1d 4096 Jan 21 13:47 .
	drwxr-xr-x.  5 root root                             4096 Jan 21 13:47 ..
	drwxr-xr-x.  4 root e9e92282a16b49e7b78d69822ac53e1d 4096 Jan 21 13:47 app-root
	drwxr-x---.  3 root e9e92282a16b49e7b78d69822ac53e1d 4096 Jan 21 13:47 .env
	drwxr-xr-x.  3 root root                             4096 Jan 21 13:47 git
	-rw-r--r--.  1 root root                               56 Jan 21 13:47 .gitconfig
	-rw-r--r--.  1 root root                             1352 Jan 21 13:47 .pearrc
	drwxr-xr-x. 10 root root                             4096 Jan 21 13:47 php-5.3
	d---------.  3 root root                             4096 Jan 21 13:47 .sandbox
	drwxr-x---.  2 root e9e92282a16b49e7b78d69822ac53e1d 4096 Jan 21 13:47 .ssh
	d---------.  3 root root                             4096 Jan 21 13:47 .tmp
	[root@node e9e92282a16b49e7b78d69822ac53e1d]# 


During a previous lab, where we setup the *rhc* tools, our SSH key was uploaded to the server to enable us to authenticate to the system without having to provide a password.  The SSH key we provided was actually appended to the *authorized_keys* file.  To verify this, use the following command to view the contents of the file:

	# cat .ssh/authorized_keys
	
You will also notice the following three directories:

* app-root - Contains your core application code as well as your data directory where persistent data is stored.
* git - Your private git repository that was created upon gear creation.
* php-5.3 - The core PHP runtime and associated configuration files.  Your application is served from this directory.

##**Understanding directory structure on the localhost**

When you created the PHP application using the *rhc app create* command, the private git repository that was created on your node host was cloned to your local machine.

	$ cd firstphp
	$ ls -al
	
You should see the following information:


	total 8
	drwxr-xr-x   9 gshipley  staff   306 Jan 21 13:48 .
	drwxr-xr-x   3 gshipley  staff   102 Jan 21 13:48 ..
	drwxr-xr-x  13 gshipley  staff   442 Jan 21 13:48 .git
	drwxr-xr-x   5 gshipley  staff   170 Jan 21 13:48 .openshift
	-rw-r--r--   1 gshipley  staff  2715 Jan 21 13:48 README
	-rw-r--r--   1 gshipley  staff     0 Jan 21 13:48 deplist.txt
	drwxr-xr-x   3 gshipley  staff   102 Jan 21 13:48 libs
	drwxr-xr-x   3 gshipley  staff   102 Jan 21 13:48 misc
	drwxr-xr-x   4 gshipley  staff   136 Jan 21 13:48 php


###**.git directory**

If you are not familiar with the git revision control system, this is where information about the git repositories that you will be interacting with is stored.  For instance, to list all of the repositories that you are currently setup to use for this project, issue the following command:

	$ cat .git/config
	
You should see the following information which specifies the URL for our repository that is hosted on the OpenShift Enterprise node host:

	[core]
		repositoryformatversion = 0
		filemode = true
		bare = false
		logallrefupdates = true
		ignorecase = true
	[remote "origin"]
		fetch = +refs/heads/*:refs/remotes/origin/*
		url = ssh://e9e92282a16b49e7b78d69822ac53e1d@firstphp-ose.example.com/~/git/firstphp.git/
	[branch "master"]
		remote = origin
		merge = refs/heads/master
	[rhc]
		app-uuid = e9e92282a16b49e7b78d69822ac53e1d


**Note:** You are also able to add other remote repositories.  This is useful for developers who also use github or have private git repositories for an existing code base.

###**.openshift directory**

The .openshift directory is a hidden directory where a user can create action hooks, set markers, and create cron jobs.  

Action hooks are scripts that are executed directly so can be written in Python, PHP, Ruby, shell, etc.  OpenShift Enterprise supports the following action hooks:

| Action Hook | Description|
| :---------------  | :------------ |
| build | Executed on your CI system if available.  Otherwise, executed before the deploy step | 
| deploy | Executed after dependencies are resolved but before application has started | 
| post_deploy | Executed after application has been deployed and started| 
| pre_build | Executed on your CI system if available.  Otherwise, executed before the build step | 
[Action Hooks][section-mmd-tables-table1] 

OpenShift Enterprise also supports the ability for a user to schedule jobs to be ran based upon the familiar cron functionality of linux.  Any scripts or jobs added to the minutely, hourly, daily, weekly or monthly directories will be ran on a scheduled basis (frequency is as indicated by the name of the directory) using run-parts.  OpenShift supports the following schedule for cron jobs:

* daily
* hourly
* minutely
* monthly
* weekly

The markers directory will allow the user to specify settings such as enabling hot deployments or which version of Java to use.

###**libs directory**

The libs directory is a location where the developer can provide any dependencies that are not able to be deployed using the standard dependency resolution system for the selected runtime.  In the case of PHP, the standard convention that OpenShift Enterprise uses is providing *PEAR* modules in the deptlist.txt file.

###**misc directory**

The misc directory is a location provided to the developer to store any application code that they do not want exposed publicly.

###**php directory**

The php directory is where all of the application code that the developer writes should be created.  By default, two files are created in this directory:

* health_check.php - A simple file to determine if the application is responding to requests
* index.php - The OpenShift template that we saw after application creation in the web browser.

##**Make a change to the PHP application and deploy updated code**

To get a good understanding of the development workflow for a user, let’s change the contents of the *index.php* template that is provided on the newly created gear.  Edit the file and look for the following code block:

	<h1>
	    Welcome to OpenShift
	</h1>

Update this code block to the following and then save your changes:

	<h1>
	    Welcome to OpenShift Enterprise
	</h1>


Once the code has been changed, we need to commit our change to the local git repository.  This is accomplished with the *git commit* command:

	$ git commit -am “Changed welcome message.”
	
Now that our code has been committed to our local repository, we need to push those changes up to our repository that is located on the node host.  

	$ git push
	
You should see the following output:

	Counting objects: 7, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (4/4), done.
	Writing objects: 100% (4/4), 395 bytes, done.
	Total 4 (delta 2), reused 0 (delta 0)
	remote: restart_on_add=false
	remote: httpd: Could not reliably determine the server's fully qualified domain name, using node.example.com for ServerName
	remote: Waiting for stop to finish
	remote: Done
	remote: restart_on_add=false
	remote: ~/git/firstphp.git ~/git/firstphp.git
	remote: ~/git/firstphp.git
	remote: Running .openshift/action_hooks/pre_build
	remote: Running .openshift/action_hooks/build
	remote: Running .openshift/action_hooks/deploy
	remote: hot_deploy_added=false
	remote: httpd: Could not reliably determine the server's fully qualified domain name, using node.example.com for ServerName
	remote: Done
	remote: Running .openshift/action_hooks/post_deploy
	To ssh://e9e92282a16b49e7b78d69822ac53e1d@firstphp-ose.example.com/~/git/firstphp.git/
	   3edf63b..edc0805  master -> master


Notice that we stop the application runtime (Apache), deploy the code, and then run any action hooks that may have been specified in the .openshift directory.  


##**Verify code change**

If you completed all of the steps in lab 16 correctly, you should be able to verify that your application was deployed correctly by opening up a web browser and entering the following URL:

	http://firstphp-ose.example.com
	
You should see the updated code for the application.

![](http://training.runcloudrun.com/images/firstphpOSE.png)

##**Adding a new PHP file**

Adding a new source code file to your OpenShift Enterprise application is an easy and straightforward process.  For instance, to create a PHP source code file that displays the server date and time, create a new file located in *php* directory and name it *time.php*.  After creating this file, add the following contents:

	<?php
	// Print the date and time
	echo date('l jS \of F Y h:i:s A');
	?>

Once you have saved this file, the process for pushing the changes involve adding the new file to your git repository, committing the change, and then pushing the code to your OpenShift Enterprise gear:

	$ git add .
	$ git commit -am “Adding time.php”
	$ git push
	
##**Verify code change**

To verify that we have created and deployed the new PHP source file correctly, open up a web browser and enter the following URL:

	http://firstphp-ose.example.com/time.php
	
You should see the updated code for the application.

![](http://training.runcloudrun.com/images/firstphpTime.png)
	
**Lab 5 Complete!**

<!--BREAK-->

#**Lab 6: Scaling an application**


**Server used:**

* localhost
* node host

**Tools used:**

* rhc
* ssh
* git
* touch
* pwd

Application scaling enables your application to react to changes in HTTP traffic and automatically allocate the necessary resources to handle the current demand. The OpenShift Enterprise infrastructure monitors incoming web traffic and automatically adds additional gear of your web cartridge online to handle requests.

##**How scaling works**

If you create a non-scaled application, the web cartridge occupies only a single gear and all traffic is sent to that gear. When you create a scaled application, it consumes two gears; one for the high-availability proxy (HAProxy) itself, and one for your actual application. If you add other cartridges like PostgreSQL or MySQL to your application, they are installed on their own dedicated gears.

The HAProxy cartridge sits between your application and the network and routes web traffic to your web cartridges. When traffic increases, HAProxy notifies the OpenShift Enterprise servers that it needs additional capacity. OpenShift checks that you have a free gear (out of your max number of gears) and then creates another copy of your web cartridge on that new gear. The code in the git repository is copied to each new gear, but the data directory begins empty. When the new cartridge copy starts it will invoke your build hooks and then HAProxy will begin routing web requests to it. If you push a code change to your web application all of the running gears will get that update.

The algorithm for scaling up and scaling down is based on the number of concurrent requests to your application. OpenShift Enterprise allocates 10 connections per gear - if HAProxy sees that you're sustaining 90% of your peak capacity, it adds another gear. If your demand falls to 50% of your peak capacity for several minutes, HAProxy removes that gear. Simple!

Because each cartridge is "share-nothing", if you want to share data between web cartridges you can use a database cartridge. Each of the gears created during scaling has access to the database and can read and write consistent data. As OpenShift Enterprise grows we anticipate adding more capabilities like shared storage, scaled databases, and shared caching. 

The OpenShift Enterprise web console shows you how many gears are currently being consumed by your application. We have lots of great things coming for web application scaling, so stay tuned.

##**Create a scaled application**

In order to create a scaled application using the *rhc* command line tools, you need to specify the *-s* switch to the command.  Let’s create a scaled PHP application with the following command:

	$ rhc app create scaledapp php-5.3 -s
	
After executing the above command, you should see output that specifies that you are using both the PHP and HAProxy cartridges:

	Password: ****
	
	Creating application 'scaledapp'
	================================
	
	  Scaling:   yes
	  Namespace: ose
	  Cartridge: php
	  Gear Size: default
	
	Your application's domain name is being propagated worldwide (this might take a minute)...
	The authenticity of host 'scaledapp-ose.example.com (10.4.59.221)' can't be established.
	RSA key fingerprint is 6c:a5:e5:fa:75:db:5a:7f:dc:a2:44:ed:e4:97:af:3c.
	Are you sure you want to continue connecting (yes/no)? yes
	Cloning into 'scaledapp'...
	done
	
	scaledapp @ http://scaledapp-ose.example.com/
	=============================================
	  Application Info
	  ================
	    UUID      = 1a6d471841d84e8aaf25222c4cdac278
	    Gear Size = small
	    Git URL   =
	ssh://1a6d471841d84e8aaf25222c4cdac278@scaledapp-ose.example.com/~/git/scaledapp.git/
	    SSH URL   = ssh://1a6d471841d84e8aaf25222c4cdac278@scaledapp-ose.example.com
	    Created   = 4:20 PM
	  Cartridges
	  ==========
	    php-5.3
	    haproxy-1.4
	  Scaling Info
	  ============
	    Scaled x2 (minimum: 2, maximum: available gears) with haproxy-1.4 on small gears
	
	RESULT:
	Application scaledapp was created.
	

![](http://training.runcloudrun.com/images/scaledApp.png)

##**Setting the scaling strategy**

OpenShift Enterprise allows users the ability to set the minimum and maximum numbers of gears that an application can use to handle increased HTTP traffic.  This scaling strategy is exposed via the web console.  While on the application details screen, click the *Scaled up with HAProxy x2* button to change the default scaling rules.

![](http://training.runcloudrun.com/images/scaledApp2.png)

##**Manual scaling**

There are often times when a developer will want to disable automatic scaling in order to manually control when a new gear is added to an application.  Some examples of when manual scaling may be preferred over automatic scaling could include:

* If you are anticipating a certain load on your application and wish to scale it accordingly. 
* You have a fixed set of resources for your application. 

OpenShift Enterprise supports this workflow by allowing users to manually add and remove gears for an application.  The instructions below describe how to disable the automatic scaling feature. It is assumed you have already created your scaled application as detailed in this lab and are at the root level directory for the application.

From your locally cloned Git repository, create a *disable autoscaling* marker, as shown in the example below:
	
	$ touch .openshift/markers/disable_auto_scaling
	$ git add .
	$ git commit -am “remove automatic scaling”
	$ git push
	
To add a new gear to your application, SSH to your application gear with the following command replacing the contents with the correct information for your application.

	$ ssh [AppUUID]@[AppName]-[DomainName].example.com

Once you have have been authenticated to your application gear, you can add a new gear with the following command:

	 $ add-gear -a [AppName] -u [AppUUID] -n [DomainName]
	 
In this lab, the application name is *scaledapp*, the application UUID is the username that you used to SSH to the node host, and the domain name is *ose*.  Given that information, your command should looking similar to the following:

	[scaledapp-ose.example.com ~]\> add-gear -a scaledapp -u 1a6d471841d84e8aaf25222c4cdac278 -n ose
	
Verify that your new gear was added to the application by running the *rhc app show* command or by looking at the application details on the web console:

	$ rhc app show scaledapp
	
After executing this command, you should see the application is now using three gears.

	scaledapp @ http://scaledapp-ose.example.com/
	=============================================
	  Application Info
	  ================
	    SSH URL   = ssh://1a6d471841d84e8aaf25222c4cdac278@scaledapp-ose.example.com
	    Gear Size = small
	    Git URL   = ssh://1a6d471841d84e8aaf25222c4cdac278@scaledapp-ose.example.com/~/git/scaledapp.git/
	    Created   = 4:20 PM
	    UUID      = 1a6d471841d84e8aaf25222c4cdac278
	  Cartridges
	  ==========
	    php-5.3
	    haproxy-1.4
	  Scaling Info
	  ============
	    Scaled x3 (minimum: 2, maximum: available gears) with haproxy-1.4 on small gears
	    
	  
![](http://training.runcloudrun.com/images/scaledApp3.png)

Just as we scaled up with the *add-gear* command, we can manually scale down with the *remove-gear* command.  Remove the third gear from your application with the following command making sure to substitute the correct application UUID:

	[scaledapp-ose.example.com ~]\> remove-gear -a scaledapp -u 1a6d471841d84e8aaf25222c4cdac278 -n ose
	
After removing the gear with the *remove-gear* command, verify that the application only contains two gears, HAProxy and a single runtime gear:

	$  rhc app show scaledapp
	
	scaledapp @ http://scaledapp-ose.example.com/
	=============================================
	  Application Info
	  ================
	    Created   = 4:20 PM
	    Gear Size = small
	    SSH URL   = ssh://1a6d471841d84e8aaf25222c4cdac278@scaledapp-ose.example.com
	    Git URL   = ssh://1a6d471841d84e8aaf25222c4cdac278@scaledapp-ose.example.com/~/git/scaledapp.git/
	    UUID      = 1a6d471841d84e8aaf25222c4cdac278
	  Cartridges
	  ==========
	    php-5.3
	    haproxy-1.4
	  Scaling Info
	  ============
	    Scaled x2 (minimum: 2, maximum: available gears) with haproxy-1.4 on small gears

##**Viewing HAProxy information**

OpenShift Enterprise provides a dashboard that will give users relevant information about the status of the HAProxy gear that is balancing and managing load between the application gears.  This dashboard provides visibility into metrics such as process id, uptime, system limits, current connections, and running tasks.  To view the HAProxy dashboard, open your web browser and enter the following URL:

	http://scaledapp-ose.example.com/haproxy-status/
	
![](http://training.runcloudrun.com/images/scaledApp4.png)


**Lab 6 Complete!**

<!--BREAK-->
#**Lab 7:  Developing Java EE applications using JBoss EAP**

**Server used:**

* localhost

**Tools used:**

* rhc
* git
* curl

OpenShift Enterprise provides the JBoss EAP runtime to facilitate the development and deployment of Java EE 6 applications.

JBoss Enterprise Application Platform 6 (JBoss EAP 6) is a fully compliant Java EE 6 platform which includes a subscription model with long-term support, platform certification, service packs and SLA(s).  In this lab we will build a simple todo application using Java EE 6 deployed on the JBoss EAP platform. The application will have a single entity called Todo and will persist todos to PostgreSQL using JPA. The application will also use EJB 3.1 Stateless session beans, Context and Dependency Injection (or CDI), and JAX RS for exposing RESTful web services.

##**Create a JBoss EAP application**

	$ rhc app create todo jbosseap
	
Just as we saw in previous labs, a template has been deployed for you at the following URL:

	http://todo-ose.example.com
	
Verify that the application has been deployed and the template is displaying correctly in your web browser.

##**Additional marker files for JBoss EAP**

If you recall from a previous lab, we discussed the way that OpenShift Enterprise allows the developer to control and manage some of the runtime features using marker files.  For Java based deployments, there are additional marker files that a developer needs to be aware of:

 * enable_jpda - Will enable the JPDA socket based transport on the JVM running the JBoss EAP application server. This enables you to remotely debug code running inside of the JBoss application server.

   * skip\_maven_build - Maven build step will be skipped
   * force\_clean_build - Will start the build process by removing all non essential Maven dependencies.  Any current dependencies specified in your pom.xml file will then be re-downloaded.
   * hot_deploy - Will prevent a JBoss container restart during build/deployment.  Newly built archives will be re-deployed automatically by the JBoss HDScanner component.
   * java7 - Will run JBoss EAP with Java7 if present. If no marker is present then the baseline Java version will be used (currently Java6)

##**Deployment directory**

If you list the contents of the application repository that was cloned to your local machine, you will notice a deployments directory.  This directory is a location where a developer can place binary archive files, .ear files for example, for deployment.  If you want to deploy a .war file rather than pushing source code, copy the .war file to deployments directory, add the .war file to your git repository, commit the change, and then push the content to your OpenShift Enterprise server.

##**Maven**

OpenShift Enterprise uses the Maven build system for all Java projects.  Once you add new source code following the standard Maven directory structure, OpenShift Enterprise will recognize the existing *pom.xml* in your applications root directory in order to build the code remotely.  

The most important thing specified in the *pom.xml* file is a Maven profile named *openshift*. This is the profile which is invoked when you do deploy the code to OpenShift Enterprise.

##**Embed PostgreSQL cartridge**

The *todo* sample application that we are going to write as part of this lab will make use of the PostgreSQL database.  Using the information that you have learned from previous labs, add the PostgreSQL cartridge to the *todo* application.

##**Building the *todo* application**

At this point, we should have an application named *todo* created as well as having PostgreSQL embedded in the application to use as our datastore.  Now we can begin working on the application.

###**Creating Domain Model**

**Note:** The source code for this application is available on github at the following URL:

	https://github.com/gshipley/todo-javaee6
	
	$ cd todo
	$ git remote add upstream -m master git://github.com/gshipley/todo-javaee6.git
	$ git pull -s recursive -X theirs upstream master
	$ git push

If you performed the above steps, your application should be ready to go and you can proceed to the **Testing the *todo* application** section.  If you like pain, you can manually code the application as show below:

The first thing that we have to do is to create the domain model for the *todo application*. The application will have a single entity named *Todo* as shown below. The entity shown below is a simple JPA entity with JPA and bean validation annotations.  Create a source file named *Todo.java* in the *todo/src/main/java/com/todo/domain* directory with the following contents:

	package com.todo.domain;

	import java.util.Date;
	import java.util.List;
	
	import javax.persistence.CollectionTable;
	import javax.persistence.Column;
	import javax.persistence.ElementCollection;
	import javax.persistence.Entity;
	import javax.persistence.FetchType;
	import javax.persistence.GeneratedValue;
	import javax.persistence.GenerationType;
	import javax.persistence.Id;
	import javax.persistence.JoinColumn;
	import javax.validation.constraints.NotNull;
	import javax.validation.constraints.Size;
	
	@Entity
	public class Todo {
	
		@Id
		@GeneratedValue(strategy = GenerationType.AUTO)
		private Long id;
	
		@NotNull
		@Size(min = 10, max = 40)
		private String todo;
		
		@ElementCollection(fetch=FetchType.EAGER)
		@CollectionTable(name = "Tags", joinColumns = @JoinColumn(name = "todo_id"))
		@Column(name = "tag")
		@NotNull
		private List<String> tags;
	
		@NotNull
		private Date createdOn = new Date();
	
		public Todo(String todo) {
			this.todo = todo;
		}
	
		public Todo() {
		}
	
		public Long getId() {
			return id;
		}
	
		public void setId(Long id) {
			this.id = id;
		}
	
		public String getTodo() {
			return todo;
		}
	
		public void setTodo(String todo) {
			this.todo = todo;
		}
	
		public Date getCreatedOn() {
			return createdOn;
		}
	
		public void setCreatedOn(Date createdOn) {
			this.createdOn = createdOn;
		}
		
		
		public void setTags(List<String> tags) {
			this.tags = tags;
		}
		
		public List<String> getTags() {
			return tags;
		}
	
		@Override
		public String toString() {
			return "Todo [id=" + id + ", todo=" + todo + ", tags=" + tags
					+ ", createdOn=" + createdOn + "]";
		}
	
	}
	
###**Create the *persistence.xml* file**

The persistence.xml file is a standard configuration file in JPA that defines your data source.  It has to be included in the *META-INF* directory inside of the JAR file that contains the entity beans. The persistence.xml file must define a persistence-unit with a unique name. Create a *META-INF* directory under src/main/resources and then create the *persistence.xml* file with the contents below:

	<?xml version="1.0" encoding="UTF-8" ?>
	<persistence xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	        xsi:schemaLocation="http://java.sun.com/xml/ns/persistence http://java.sun.com/xml/ns/persistence/persistence_2_0.xsd"
	        version="2.0" xmlns="http://java.sun.com/xml/ns/persistence">
	
	        <persistence-unit name="todos" transaction-type="JTA">
	                <provider>org.hibernate.ejb.HibernatePersistence</provider>
	                <jta-data-source>java:jboss/datasources/PostgreSQLDS</jta-data-source>
	                <class>com.todo.domain.Todo</class>
	                <properties>
	                        <property name="hibernate.show_sql" value="true" />
	                        <property name="hibernate.hbm2ddl.auto" value="create" />
	                </properties>
	
	        </persistence-unit>
	</persistence>

The *jta-data-source* refers to JNDI name preconfigured by OpenShift Enterprise in the standalone.xml file located in the *.openshift/config* directory.

###**Create the TodoService EJB bean**

Next we will create a stateless EJB bean named *TodoService* in the *com.todo.service package*.  This bean will perform basic CRUD operations using *javax.persistence.EntityManager*.  Create a file named *TodoService* in the *src/main/java/com/todo/service* directory and add the following contents:

	package com.todo.service;
	
	import java.util.List;
	import javax.ejb.Stateless;
	import javax.persistence.EntityManager;
	import javax.persistence.PersistenceContext;
	import com.todo.domain.Todo;
	
	@Stateless
	public class TodoService {
	
	        @PersistenceContext
	        private EntityManager entityManager;
	
	
	        public Todo create(Todo todo) {
	                entityManager.persist(todo);
	                return todo;
	        }
	
	        public Todo find(Long id) {
	                Todo todo = entityManager.find(Todo.class, id);
	                List<String> tags = todo.getTags();
	                System.out.println("Tags : " + tags);
	                return todo;
	        }
	}
	
###**Enable CDI**

CDI or Context and Dependency Injection is a Java EE 6 specification which enables dependency injection in a Java EE 6 project. To enable CDI in the *todo* project, create a *beans.xml* file in *src/main/webapp/WEB-INF* directory with the following contents:

	<?xml version="1.0"?>
	<beans xmlns="http://java.sun.com/xml/ns/javaee"
	 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://jboss.org/schema/cdi/beans_1_0.xsd"/>

In order to use the *@Inject* annotation instead of the *@Ejb* annotation to inject an EJB, you will have to write a producer which will expose the *EntityManager*.  Create a source file in the *src/main/java/com/todo/utils* directory named *Resources* and add the following source code:

	package com.todo.utils;
	
	import javax.enterprise.inject.Produces;
	import javax.persistence.EntityManager;
	import javax.persistence.PersistenceContext;
	
	public class Resources {
	
	    @Produces
	    @PersistenceContext
	    private EntityManager em;
	
	}

###**Creating a RESTful web service**

Before exposing a RESTful web service for the *Todo* entity, we need to enable JAX-RS in our application. To enable JAX-RS, create a class which extends *javax.ws.rs.core.Application* and specify the application path using a *javax.ws.rs.ApplicationPath* annotation.  Create a source file named *JaxRsActivator* in the *src/main/java/com/todo/rest* directory and add the following source code:

	package com.todo.rest;
	
	import javax.ws.rs.ApplicationPath;
	import javax.ws.rs.core.Application;
	
	@ApplicationPath(“/rest”)
	public class JaxRsActivator extends Application {
	   /* class body intentionally left blank */
	}


Next we will create a *TodoRestService* class which will expose two methods that will create and read a *Todo* object. The service will consume and produce JSON.  Create a source file named *TodoRestService* in the *src/main/java/com/todo/rest* directory and add the following source code:

	package com.todo.rest;
	
	import javax.inject.Inject;
	import javax.ws.rs.Consumes;
	import javax.ws.rs.GET;
	import javax.ws.rs.POST;
	import javax.ws.rs.Path;
	import javax.ws.rs.PathParam;
	import javax.ws.rs.Produces;
	import javax.ws.rs.WebApplicationException;
	import javax.ws.rs.core.MediaType;
	import javax.ws.rs.core.Response;
	import javax.ws.rs.core.UriBuilder;
	import com.todo.domain.Todo;
	import com.todo.service.TodoService;
	
	@Path("/todos")
	public class TodoRestService {
	
		@Inject
		private TodoService todoService;
	
		@POST
		@Consumes("application/json")
		public Response create(Todo entity) {
			todoService.create(entity);
			return Response.created(
					UriBuilder.fromResource(TodoRestService.class)
							.path(String.valueOf(entity.getId())).build()).build();
		}
	
		@GET
		@Path("/{id:[0-9][0-9]*}")
		@Produces(MediaType.APPLICATION_JSON)
		public Todo lookupTodoById(@PathParam("id") long id) {
			Todo todo = todoService.find(id);
			if (todo == null) {
				throw new WebApplicationException(Response.Status.NOT_FOUND);
			}
			return todo;
		}
	}
	
##**Deploy the *todo* application to OpenShift Enterprise**

Now that we have our application created, we need to push our changes to the OpenShift Enterprise gear that we created earlier in this lab.  From the application root directory, issue the following commands:

	$ git add .
	$ git commit -am “Adding source code”
	$ git push
	
Once you execute the *git push* command, the application will begin building on the OpenShift Enterprise node host.  During this training class, the OpenStack virtual machines we have created are not production grade environments.  Because of this, the build process will take some time to complete.  Sit back, be patient, and help your fellow classmates who may be having problems.

##**Testing the *todo* application**

In order to test out the RESTful web service that we created in this lab, we can add and retrieve todo items using the *curl* command line utility.  To add a new item, enter the following command:

	$ curl -k -i -X POST -H "Content-Type: application/json" -d '{"todo”:”Buy a lot of OpenShift Enterprise","tags":["javascript","ui"]}' https://todo-ose.example.com/rest/todos
	
To list all available todo items, run the following command:

	$ curl -k -i -H "Accept: application/json" https://todo-ose.example.com/rest/todos/1
	
You should see the following output:

	HTTP/1.1 200 OK
	Date: Fri, 25 Jan 2013 04:05:51 GMT
	Server: Apache-Coyote/1.1
	Content-Type: application/json
	Connection: close
	Transfer-Encoding: chunked
	
	{"id":1,"todo":"Sell a lot of OpenShift Enterprise","tags":["javascript","ui"],"createdOn":1359086546955}
	
If you downloaded and deployed the source code from the git repository, the project contains a JSF UI component which will allow you to test the application using your web browser.  Simply point your browser to

	http://todo-ose.example.com
	
to verify that the application was deployed correctly.

##**Extra Credit**

SSH into the application gear and verify the todo item was added to the PostgreSQL database.


**Lab 7 Complete!**
<!--BREAK-->



