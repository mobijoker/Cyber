---
lang: en
ref: creating-public-private-key-authentication-for-ssh
title: Creating public/private key authentication for SSH
date: 2014-06-14T02:50:19+00:00
author: Arthur Gareginyan
layout: post
permalink: /linux/creating-public-private-key-authentication-for-ssh.html
categories:
  - Debian/Ubuntu
  - Linux
  - Mac OS
  - Raspberry Pi
tags:
  - authentication
  - authorize
  - debian
  - key
  - mac
  - mac os
  - password
  - pub
  - pub key
  - raspbian
  - ssh
  - ubuntu

---

![thumb](/images/ssh-key-300x300.png)
If you use ssh to connect to the remote host, one way to ensure the security of the connection is the use of public/private SSH key, because password is not passed across the network and the system is resistant to attacks by "brute force".

Create a public/private SSH key in Linux or Mac OS is very simple.
 
 
### On the local machine

If needed create a .ssh directory in our home directory:

```
mkdir ~/.ssh
```

Create the SSH keys. Enter the command below and press enter, when asked for a pass phrase leave blank, since our purpose is to automate things:

```
ssh-keygen -t rsa
```

Or we can choose DSA (Digital Signing Algorithm) instead of RSA:

```
ssh-keygen -t dsa
```

There will be created two files in the .ssh directory: `id_dsa` and `id_dsa.pub`. The pub file has the public key and will be placed on the remote server.

Copy the `id_dsa.pub` file to the remote server via SCP:

```
scp ~/.ssh/id_dsa.pub username@example.com:/home/username/
```


### On the remote server

Connect to the remote server with SSH:

```
ssh username@example.com
```

If needed create a .ssh directory in our home directory:

```
mkdir ~/.ssh
```

Copy the public key to the file <strong>authorized_keys</strong>:

```
cat id_dsa.pub >> ~/.ssh/authorized_keys
```

Remove file `id_dsa.pub`:

```
rm id_dsa.pub
```

Setting the correct permissions on the key:

```
chown -R username:username /home/username/.ssh
chmod 700 /home/username/.ssh
chmod 600 /home/username/.ssh/authorized_keys
```

Open the configuration file of SSH:

```
sudo nano /etc/ssh/sshd_config
```

And check this lines:

<pre>
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile      %h/.ssh/authorized_keys
PasswordAuthentication no
</pre>

Restart the server SSH:

```
sudo /etc/init.d/ssh reload
```

Done.

And now you can connect to the remote server with SSH:

```
ssh -i /path-to-private-key username@remote-host-ip-address
```

Or just this:

```
ssh username@remote-host-ip-address
```
