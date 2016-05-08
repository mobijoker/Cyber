---
id: 606
lang: en
ref: antivirus-on-a-linux-machine
title: Antivirus on a Linux machine
date: 2015-05-31T04:44:30+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=606
permalink: /linux/antivirus-on-a-linux-machine.html
switch_like_status:
  - 1
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - antivirus
  - clam
  - clam antivirus
  - clamav
  - freshclam
  - malicious threats
  - malware
  - trojan
  - вирус
  - вредоносная программа
  - троян

---

![thumb](/images/clamav-trademark-300x244.png)
How to, on a Linux machine, using the ClamAV, detect malicious code (trojans, viruses, malware & other malicious threats).


ClamAV (Clam AntiVirus) - is an open source antivirus engine for detecting trojans, viruses, malware & other malicious threats on mail servers, but it can also be used on desktops.


### Installation

It’s included in the Debian repositories, so installation is simple:

```
sudo apt-get update
sudo apt-get install clamav
```

### Using

Before scanning, you must update the virus signature database:

```
sudo freshclam
```

<pre>
ClamAV update process started at Tue May 19 17:02:33 2015
main.cvd is up to date (version: 55, sigs: 2424225, f-level: 60, builder: neo)
Downloading daily-20485.cdiff [100%]
daily.cld updated (version: 20485, sigs: 1392599, f-level: 63, builder: neo)
bytecode.cld is up to date (version: 256, sigs: 45, f-level: 63, builder: dgoddard)
Database updated (3816869 signatures) from db.local.clamav.net (IP: 198.148.78.4)
</pre>

Now you can scan any directory (such as `/home`) for a viruses:

```
clamscan -r -i /home
```

* **-r** - Scan directories recursively.
* **-i** - Show only infected files.
* **/home** - Directory of scanning.

**Note:** To scan the entire system (`/`) you must to run a program as root (using sudo).

**Note:** This command will only show the infected files, but will not clean them (remove virus from file), send to quarantine or delete.

The utility clamscan have many additional options for scanning. Example:

* **--bell** - Sound bell on virus detection.
* **--log** - Write log.
* **--max-dir-recursion** - The maximum depth of search in directories.
* **--exclude-dir** - Don't scan directory.
* **--copy** - Copy infected  files into directory.
* **--move** - Move infected  files into directory.
* **--remove** - Remove infected files. Be careful!

To learn about ClamAv's other options try `man`:

```
man clamscan
```

An example of the use of additional parameters:

```
sudo clamscan -ri --bell --max-dir-recursion=50 --move=/home/user/INFECTED/ --log=/var/log/clamav/clamav.log --exclude-dir=/mnt/storage/ /
```


</br><h4>Automation</h4>

To automate the scanning, you can use the Cron task scheduler. To do this, you need to enter several lines in the file `/etc/crontab`.

```
sudo nano /etc/crontab
```

<pre>
# ClamAV
0  3    * * *   root    /usr/bin/freshclam
20 3    * * *   root    /usr/bin/clamscan -r /
</pre>

Now scanning will occur automatically every day at 3:0. A twenty minute period required to complete the freshclam (update the database).

**Note:** Set any time you like and replace the string `/usr/bin/clamscan -r /` to necessary.


### Possible finds

The scan can detect these "viruses":

<pre>
PUA.Script.Packed-1 FOUND
PUA.Script.Packed-2 FOUND
</pre>

In fact, this is not a virus.

* PUA  - Possibly Unwanted Applications.
* Script.Packed - The script is packed (archived).

To disable detection of PUA use an additional parameter:

<pre>
--detect-pua=no
</pre>

And to enable detection of PUA:

<pre>
--detect-pua=yes
</pre>

Example:

```
sudo clamscan -r -i --detect-pua=yes / 
```


### Possible errors

#### ERROR 1

When you update the virus signature database, it can return this error message:

```
freshclam
```

<pre>
ERROR: Can't open /var/log/clamav/freshclam.log in append mode (check permissions!).
ERROR: Problem with internal logger (UpdateLogFile = /var/log/clamav/freshclam.log).
</pre>

This is because the user was running freshclam without certain rights. This is solved by running freshclam with sudo:

```
sudo freshclam
```

#### ERROR 2

Scanning can return this error message:

<pre>
LibClamAV Warning: fmap_readpage: pread fail: asked for 4085 bytes @ offset 11, got 0
LibClamAV Warning: fmap_readpage: pread fail: asked for 4091 bytes @ offset 5, got 0
LibClamAV Warning: fmap_readpage: pread fail: asked for 4094 bytes @ offset 2, got 0
LibClamAV Error: fmap_readpage: pread error: Input/output error
</pre>

For this to not happen, you must to exclude from scanning several directories, like so:

```
sudo clamscan -ir --exclude-dir=^/sys --exclude-dir=^/dev --exclude-dir=^/proc /
```
