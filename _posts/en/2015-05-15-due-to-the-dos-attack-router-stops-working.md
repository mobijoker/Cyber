---
id: 580
lang: en
ref: due-to-the-dos-attack-router-stops-working
title: Due to the DoS attack router stops working
date: 2015-05-15T09:48:14+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=580
permalink: /linux/due-to-the-dos-attack-router-stops-working.html
switch_like_status:
  - 1
categories:
  - Error
  - Hacking
  - Linux
  - Электроника
tags:
  - asus
  - attack
  - DoS
  - dos-attack
  - log
  - logs
  - router
  - RT-N12
  - RT-N12E
  - RT-N12LX
  - shell

---

![thumb](/images/DoS-attack-and-wireless-router-300x300.png)
How to fix the issue if, in the logs of the router, you see the message about a DoS attacks and then your ASUS router is down until you reboot it.


Recently I was faced with such a problem. Sometimes, the Internet has been disconnected and web interface of the router stopped working. Connect to a Wi-Fi network is not lost. After rebooting the router everything went normally. But after a while, the situation was repeated. And, in the system logs, many rows about the DoS attacks.

<pre>
May 13 00:03:41 rlx-linux user.warn kernel: DoS: Port Scan Attack source=00.00.00.00 destination=00.00.00.00
May 13 00:03:42 rlx-linux user.warn kernel: DoS: Port Scan Attack source=00.00.00.00 destination=00.00.00.00
May 13 00:03:52 rlx-linux user.warn kernel: DoS: Port Scan Attack source=00.00.00.00 destination=00.00.00.00
</pre>

Do not need to worry about these attacks, if the router has protection from them. My router has this feature. But better is to find out the cause of these attacks. Such records in the logs does not necessarily mean that it is an attack, there are also other reasons for their occurrence.

The problem was in another. As attacks have been constant (every second), then the router not coping with the logging of information about them in the system logs. Therefore, if it is not possible to eliminate the cause of the attacks, then you can disable the logging of information about attacks.

I have the router Asus RT-N12LX. The web interface of the router doesn’t have a trigger to control or disable loging. So needed to get access to command line of the router. The most secure way is using the SSH protocol, but we can use insecure Telnet as that's all ASUS ship with it by default. If the web-interface of your router don’t have the trigger to enable Telnet, then you need to read this article: <a href="http://mycyberuniverse.com/linux/enable-telnet-on-the-asus-rt-n12e-lx-router.html" target="_blank">«How to enable the Telnet server on the ASUS router»</a>.

First of all, we will find all variables with word "LOG" in the NVRAM (Non Volatile Random Access Memory):

```
flash all | grep LOG
```

<pre>
DEF_SCRLOG_ENABLED=3
DEF_REMOTELOG_ENABLED=0
DEF_REMOTELOG_SERVER=""
SCRLOG_ENABLED=3
REMOTELOG_ENABLED=0
REMOTELOG_SERVER=""
Aborted
</pre>

Needed variable is `SCRLOG_ENABLED`. The value of this variable is 3, that is a level of logging and we can reduce it to 2 or 1. If this does not help then we can set it to 0 for completely disable the logging.

So, to reduce the level of logging, run this:

```
flash set SCRLOG_ENABLED 2
```

or this:

```
flash set SCRLOG_ENABLED 1
```

And to completely disable the logging, run this:

```
flash set SCRLOG_ENABLED 0
```

Now, you must reboot your router, for the changes to take effect:

```
reboot
```

All previous logs will be automatically deleted after the reboot, but if you need to immediately delete (before the reboot) it then run this:

```
rm /var/log/messages*
```

And, you can run this to show all logs from console:

```
ls /var/log/
```
