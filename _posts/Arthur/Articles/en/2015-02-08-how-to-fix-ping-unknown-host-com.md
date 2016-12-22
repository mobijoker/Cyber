---
lang: en
ref: how-to-fix-ping-unknown-host-com
title: 'How to fix: “ping: unknown host ***.com”'
date: 2015-02-08
author: Arthur Gareginyan
layout: post
permalink: /linux/how-to-fix-ping-unknown-host-com.html
switch_like_status:
  - 1
categories:
  - Debian/Ubuntu
  - Error
  - Linux
  - Raspberry Pi
tags:
  - fix
  - how to fix
  - ping
  - unknown host

---

![thumb](/images/thumbnail/error.png)
How to fix the issue if you see the message about the host is unknown when attempting to ping a domain name.


I can ping one of Google's servers:

<pre>
$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_req=1 ttl=51 time=8.09 ms
64 bytes from 8.8.8.8: icmp_req=2 ttl=51 time=8.34 ms
64 bytes from 8.8.8.8: icmp_req=3 ttl=51 time=12.4 ms
</pre>

But I can't resolve any domain names:

<pre>
$ ping google.com
ping: unknown host google.com
</pre>

This means that resolving of the domain names to IP via DNS (Domain Name System) is not working.

To fix this, simply type the following command:

```
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
```

Or you can manual edit the `resolv.conf` file. For this you need to open the `resolv.conf` file:

```
sudo nano /etc/resolv.conf
```

And add this line instead of what ever you have:

<pre>
nameserver 8.8.8.8
</pre>

> **Note:** `8.8.8.8` - is a Google DNS servers.
