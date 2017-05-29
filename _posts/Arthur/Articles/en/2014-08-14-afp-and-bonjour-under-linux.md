---
lang: en
ref: afp-and-bonjour-under-linux
title: AFP and Bonjour under Linux
date: 2014-08-14
author: Arthur Gareginyan
layout: post
permalink: /linux/afp-and-bonjour-under-linux.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - AFP
  - Apple Filing Protocol
  - Avahi
  - Avahi-daemon
  - Bonjour
  - file server
  - linux
  - mac
  - mac os
  - Netatalk
  - sharing

---

![thumb](/images/thumbnail/time-capsule.png)
For quite some time I use my Linux machine as a file and backup server (Mac File Server and Time Machine Volume) for all Mac’s in my network which is accessible from the Finder in Mac OS X.


We will use the following packages to implement the needed features on Linux mashine:

* The analog of the `Apple Filing Protocol (AFP)` in Linux is the `Netatalk`.
* The analog of the `Bonjour` in Linux is the `Avahi`.


### Install and configure Netatalk

Netatalk is the Open Source implementation of AFP.

Install Netatalk:

```
sudo apt-get install netatalk
```

First we should deactivate services provided by Netatalk which are not needed.

```
sudo nano /etc/default/netatalk
```

Locate the following startup options and change them as noted below:

<pre>
ATALKD_RUN=no
PAPD_RUN=no
CNID_METAD_RUN=yes
AFPD_RUN=yes
TIMELORD_RUN=no
A2BOOT_RUN=no
</pre>


### Configure shared Volumes

Now we have to tell the afpd daemon what volumes we want to share.

```
sudo nano /etc/netatalk/AppleVolumes.default
```

Scroll to the bottom of the document and define your shared volumes:

<pre>
~/                      		"Home Directory"
</pre>

You can setup as many shared volumes as you wish. You can even define which users are allowed to access each share. You do this using the allow option.

On my server, I have the following setup for my external drive.

<pre>
~/Drive/                		"Drive" allow:berserkr,milena
</pre>

Since you’ll probably want to use your file server as a time machine backup, we can also define a volume just for that. Create a directory `TimeMachine`, and set it up using the following line.

<pre>
~/Drive/TimeMachine     	"TimeMachine" allow:berserkr,milena  options:tm
</pre>

Finally restart Netatalk to activate the changes:

```
sudo /etc/init.d/netatalk restart
```

Now we have a fully configured AFP it will not show up in the Finder sidebar on OS X, it is however reachable via `Go` -&gt; `Connect to Server` in Finder.


### Install and configure Avahi

OS X use a service called Bonjour for automatic discovery, which displays the server on your sidebar. Linux can emulate this functionality with an open source implementation of Bonjour called Avahi.

Install Avahi:

```
sudo apt-get install avahi-daemon
```

Create a xml-file for the afpd service with the following line:

```
sudo nano /etc/avahi/services/afpd.service
```


```
<?xml version="1.0" standalone='no'?><!--*-nxml-*-->
<!DOCTYPE service-group SYSTEM "avahi-service.dtd">
<service-group>
  <name replace-wildcards="yes">%h</name>

  <service>
    <type>_afpovertcp._tcp</type>
    <port>548</port>
  </service>

  <service>
    <type>_device-info._tcp</type>
    <port>0</port>
    <txt-record>model=TimeCapsule</txt-record>
  </service>

</service-group>
```

Restart the avahi daemon to activate all changes:

```
sudo /etc/init.d/avahi-daemon restart
```

Now you have configured the Avahi daemon to advertise AFP sharing across your network which will cause your Linux machine to show up in Finder’s sidebar.


### Configure Time Machine on Mac OS

Just choose a TimeMachine volume as the backup disk in the Time Machine system preferences. That’s it!
