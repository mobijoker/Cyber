---
lang: en
ref: secure-copying-files-via-ssh
title: Secure copying files via SSH
date: 2015-03-05
author: Arthur Gareginyan
layout: post
permalink: /linux/secure-copying-files-via-ssh.html
categories:
  - DD-WRT
  - Debian/Ubuntu
  - Linux
  - Mac OS
  - Raspberry Pi
tags:
  - OpenSSH
  - SCP
  - secure copy
  - ssh

---

![thumb](/images/thumbnail/copy-files.png)
How to, from the terminal, securely transfer data between a local host and a remote host or between two remote hosts.


SCP (Secure CoPy) - is a console program to perform a remotely copying files between hosts. It is based on the Secure Shell (SSH) protocol and provides the same authentication and same level of security as SSH.

While copying the source file to a destination, if the destination file is already exists, then SCP overwrites it. If the destination file does not already exist, then SCP create a blank file with the destination file name and write the contents of the copied file.

Typically, a syntax of scp program is like the syntax of cp (copy) program.


### Example syntax for SCP

Copying the file to the home directory of the user on the remote host:

```sh
scp SourceFile user@remote.host:
```

Copying file to the specified directory on the remote host:

```sh
scp SourceFile user@remote.host:directory/TargetDir
```

Copying file from remote host:

```sh
scp user@remote.host:directory/SourceFile TargetFile
```

Copying directory to remote host:

```sh
scp -r SourceDir user@remote.host:directory/TargetDir
```

Copying directory from remote host:

```sh
scp -r user@remote.host:directory/SourceDir TargetDir
```

Copying file from one remote host to another remote host:

```sh
scp user@remote.host1:/directory/SourceFile user@remote.host2:/directory/
```

Copying multiple files to remote host:

```sh
scp SourceFile1 SourceFile2 user@remote.host:
```

Copying multiple files from remote host:

```sh
scp user@remote.host:~/\{SourceFile1, SourceFile2, SourceFile3\} .
```

Copying file to remote host with port 2222 (default is 22):

```sh
scp -P 2222 user@host:directory/SourceFile TargetFile
```

Copying file with saving the creating time, modification time and permissions to the remote host:

```sh
scp -p SourceFile user@remote.host:
```


### SCP Performance

Copying file with Blowfish encryption (default is AES-128) to remote host:

```sh
scp -c blowfish SourceFile user@remote.host:
```

Copying file with limit the bandwidth to 100 Kbit/s to the remote host:

```sh
scp -l 100 SourceFile user@remote.host:
```
