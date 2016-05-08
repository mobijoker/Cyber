---
id: 508
lang: en
ref: connect-to-raspberry-pi-from-a-mac-using-ethernet
title: Connect to Raspberry Pi from a Mac using Ethernet
date: 2015-02-03T21:44:05+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=508
permalink: /mac-os/connect-to-raspberry-pi-from-a-mac-using-ethernet.html
categories:
  - Mac OS
  - Raspberry Pi
tags:
  - ethernet
  - mac
  - mac os
  - OpenSSH
  - raspberry
  - raspberrypi
  - raspbian
  - ssh

---

![thumb](/images/Raspberry_Pi_Logo-e1422999720343.png)
The Raspberry Pi is a great single board computer. However I don't always want to hook up the Raspberry Pi to some screen and keyboard when working with it. I like to do everything using SSH which is enabled out of the box if you are using the Raspbian distribution. So just hook up it to your router and start hacking. But what if now you don't have router and only have the Mac?


The Raspbian is configured by default to receive an IP address from a DHCP server. So you need a DHCP server. This can be done using the sharing option in Mac OS X. Just set it up like that.
<img class="aligncenter wp-image-509 size-full" src="/images/Screen-Shot-2015-02-03-at-23.27.19.png" alt="Mac OS X Sharing" width="782" height="662" />

Once you have enabled this option just connect your Mac and Raspberry Pi using an ethernet cable. Also note that you don't need a special “cross-over” cable.

Now you can login to the Raspberry Pi at **IP-address** `192.168.2.2` with **Username:** `pi`, **Password:** `raspberry`.

**1.** Open up a new Terminal on your Mac.

**2.** Connect to Raspberry Pi:

```
ssh pi@192.168.2.2
```

**3.** You’ll be prompted to verify you’re trying to login to the Raspberry Pi. Type `yes` an press return.

**4.** Type the password. The default password for the Raspbian image is `raspberry`. Type `raspberry` and press return.

You’re logged into your Raspberry Pi!
