---
lang: en
ref: how-to-fix-host-key-verification-failed
title: 'How to fix: “Host key verification failed”'
date: 2015-02-05T10:49:51+00:00
author: Arthur Gareginyan
layout: post
permalink: /linux/how-to-fix-host-key-verification-failed.html
categories:
  - Debian/Ubuntu
  - Error
  - Linux
  - Mac OS
  - Raspberry Pi
tags:
  - error
  - fix
  - host key
  - how to fix
  - key
  - known_hosts
  - ssh

---

![thumb](/images/error.png)
When attempting to connect using SSH, the connection may be automatically rejected with the following error:
<pre>
Host key verification failed
</pre>


After rebuilding a web-server, I tried to login into it via SSH and have received the following error:

	@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
	@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
	@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
	IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
	Someone could be eavesdropping on you right now (man-in-the-middle 	attack)!
	It is also possible that the RSA host key has just been changed.
	The fingerprint for the RSA key sent by the remote host is
	NN:NN:NN:NN:NN:NN:NN:NN:NN:NN:NN:NN:NN:NN:NN:NN.
	Please contact your system administrator.
	Add correct host key in /Users/Arthur/.ssh/known_hosts to get rid of this message.
	Offending key in /Users/Arthur/.ssh/known_hosts:8
	RSA host key for [192.168.2.2]:22 has changed and you have requested strict checking.
	Host key verification failed.

"Host key verification failed" means that the host key of the remote host was changed since you ssh to it in last time and so the system does not allow access for security purposes.

So you need to change the host key in the known_hosts file. But no need to delete the known_hosts file, for example, by using the following command:

```
rm -f /home/user/.ssh/known_hosts
```

The message already told you what to do. To correct it, take a look at the last integer of the line that says “Offending ECDSA key,” because this integer is actually the line number inside your known_hosts file that’s throwing the error. Simply type the following command:

```
sed -i '8d' ~/.ssh/known_hosts
```

Where `8d` is the line number, so if your line number another then you need to use another number, for example `2d`.

Or you can manual edit the `known_hosts` file. For this you need to open the `known_hosts` file and manual delete the line that’s throwing the error.

```
sudo nano .ssh/known_hosts
```
