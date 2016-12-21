---
title: 'How to fix: No matching key exchange method found by OpenSSH 7.0'
ref: no-matching-key-exchange-method-found-openssh7
permalink: /error/no-matching-key-exchange-method-found-openssh7.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - error
tags:
  - fix
  - how to fix
  - error
  - issue
  - problem
  - ssh
  - openssh7
  - openssh 7
  - openssh 7.0
  - diffie-hellman-group1-sha1
  - unable to negotiate with
  - no matching key exchange method found
  - Logjam attack
  - key exchange algorithm

---

![thumb](/images/thumbnail/error.png)
After update to new release of SSH, when trying to connect to my server by using SSH, I get the following message:
<pre>
Unable to negotiate with 192.168.1.1 port 22: no matching key exchange method found.
Their offer: diffie-hellman-group1-sha1
</pre>


<br>

### What causes this problem

OpenSSH 7.0 deprecated the `diffie-hellman-group1-sha1` key algorithm because it is weak and within theoretical range of the so-called Logjam attack. See the [www.openssh.com/legacy.html](http://www.openssh.com/legacy.html) page for more information.

If the client and server are unable to agree on a mutual set of parameters then the connection will fail. OpenSSH (7.0 and greater) will produce an error message like this:

<pre>
Unable to negotiate with host: no matching key exchange method found.
Their offer: diffie-hellman-group1-sha1
</pre>

In this case, the client and server were unable to agree on the key exchange algorithm because the server offered only a single method `diffie-hellman-group1-sha1`.


### How to fix it

The best resolution for these failures is to upgrade/configure the server to not use deprecated algorithms. If that is not possible, you can force the client to re-enable the `diffie-hellman-group1-sha1` key exchange algorithm with the `-oKexAlgorithms=+diffie-hellman-group1-sha1` option on the command-line:

```
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 user@host
```

or in the `~/.ssh/config` file:

```
Host somehost.example.org
	KexAlgorithms +diffie-hellman-group1-sha1
```
