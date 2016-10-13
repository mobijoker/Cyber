---
lang: en
ref: chistka-linux
title: Clean Linux
date: 2013-07-04
author: Arthur Gareginyan
layout: post
permalink: /linux/chistka-linux.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi

---

![thumb](/images/thumbnail/Clean-linux.png)
Clean Linux from debris.
 

### Determination of the amount of used and free space.

We define the amount of used and free space on the disk:

```
df -h
```

**Note:**
The parameter "h" is needed to display the data in familiar megabytes.

In the command output will be information about what amount of disk space on all mounted file systems, how busy and how much more freely.

We define the amount of used and free space on the disc:

```
df -h /dev/sda1
```

**Note:**
The program "df" only displays information about the mounted devices and partitions.


### Determination of the number and volume of the specified files and directories.

The program "du" lets you know how much space take a particular file or directory. It is useful for determining the largest files and directories as candidates for removal in the struggle for space.

Example:

```
du -ms /home/user/
```

*Note:*

* The parameter "m" is needed to display the data in a familiar megabytes. 
* The parameter "s" is necessary to show only the total volume of the catalog.

If you do not use paremetr "s" while in the output will be data on the volume of each subdirectory and file in the specified directory.

```
du -m /home/user/
```

With the parameter "S" in the output will only information about the volume of sub-directories but not files. 

```
du -mS /home/user/
```


### Cleaning the basket from the console.

We find all the debris in the system:

```
locate Trash
```

**Note:**
It is "Trash" and not "trash"

Empty Trash in full:

```
sudo rm -rf ~/.local/share/Trash/files/*
```

*Note:*

* The parameter "r" is used to recursively remove (delete subdirectories with file attachments). 
* The parameter "f" (force) is used to ignore errors related to non-existent files and for that did not request confirmation of transactions.
* ~/.local/share/Trash/files/ –The way in which files are deleted (garbage in the cart). A tilde and a slash (~ /) short address of the home directory to use instead of “/home/user/”.

I use a program file synchronization BitTorrentSync who has his cart along the way home/user/btsync/.SyncTrash/.
Empty Trash BitTorrentSync:

```
sudo rm -rf ~/btsync/.SyncTrash/*
```


### Cache cleaning apt.

All ever downloaded us packages (apt) fold on our disk in the local repository and automatically never removed.

**apt-get clean** - Command "clean" is used to free up disk space by purification packets received from a local repository,in other words clears the cache apt located on the path /var/cache/apt/archives/

**apt-get autoclean** - It differs from the "clean" in that what deletes the cache those packages, that can no longer be downloaded (eg older versions of packages), and thus useless.

**apt-get autoremove** - The command autoremove  is used to  automatically remove packages which were set to satisfy dependencies for other packages and  now no longer needed.

Clean up a local repository from unwanted software and remove unnecessary dependencies:

```
sudo apt-get autoclean
sudo apt-get autoremove
```

Or cleanse local repository fully and remove unnecessary dependencies:

```
sudo apt-get clean
sudo apt-get autoremove
```
