---
layout: reference
title: Install TextTest on Amazon Linux
---

# Install TextTest on Amazon Linux

Detailed instructions follow.

## Provision a machine - Amazon Linux
First provision a Linux 2 box using the AWS tooling. If you want to run an IDE on it you need 8GB ram and 16 GB hard drive. 

Follow [these instructions](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-linux-2-install-gui/) to enable VNC.

At this point you should be able to use VNC to connect to your EC2 machine. I used [Real VNC]( https://www.realvnc.com/en/connect/download/viewer/macos/)

To change the vnc password for a machine, use 'vncpasswd'. I usually make it the same as the name of the pem file.

When you've got the machine up and running you should be able to open an ssh tunnel to it with a command similar to this one (use your own pem file and ip address):

	ssh -L 5901:localhost:5901   -i yourkeyfile.pem ec2-user@ip_address


## Install TextTest and pyGTK

Install python3: 

	sudo yum install python3

Install gobject using the commands below. Note: there are instructions [here](https://pygobject.readthedocs.io/en/latest/getting_started.html#fedora-logo-fedora) but don't follow them since they only partially work. The crucial missing step is to install 'cairo-gobject-devel' as I discovered from [this page](https://stackoverflow.com/questions/55735783/add-the-directory-containing-cairo-gobject-pc). Do this instead:

	sudo yum install gcc gobject-introspection-devel cairo-devel pkg-config python3-devel gtk3
	sudo yum install cairo-gobject-devel
	sudo pip3 install texttest
	sudo pip3 install pycairo
	sudo pip3 install PyGObject

Now you should be able to connect to the machine with VNC, open a terminal and run `texttest --new` which should open a new texttest window. Close it for the moment while you install the supporting tools and configure your personal config file as explained below.

## Install supporting tools

The following tools are very useful to have alongside TextTest.

### Git

	sudo yum install git

### Sublime text

[Instructions for yum](https://www.sublimetext.com/docs/3/linux_repositories.html). 

### Meld
Download the rpm and install it. [This page](https://centos.pkgs.org/7/epel-x86_64/meld-3.16.4-2.el7.noarch.rpm.html) lists it, use curl to download it - [this page](https://centos.pkgs.org/7/epel-aarch64/meld-3.16.4-2.el7.noarch.rpm) has a link to the actual rpm. For example:

	curl https://download-ib01.fedoraproject.org/pub/epel/7/aarch64/Packages/m/meld-3.16.4-2.el7.noarch.rpm > meld.rpm
	sudo yum install meld.rpm

### Chrome
See these [instructions](https://linuxize.com/post/how-to-install-google-chrome-web-browser-on-centos-7/)

## Configure TextTest to use the supporting tools
Set up your [personal texttest config file](../how_to_guides/configure_editor.html) to use meld and sublime:

	view_program:subl
	diff_program:meld

Now when you start texttest you should be in a good position to use it to run and develop test cases.
