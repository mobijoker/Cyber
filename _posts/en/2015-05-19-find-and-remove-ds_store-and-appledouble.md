---
lang: en
ref: find-and-remove-ds_store-and-appledouble
title: Find and remove .DS_Store and .AppleDouble
date: 2015-05-19T08:41:32+00:00
author: Arthur Gareginyan
layout: post
permalink: /mac-os/find-and-remove-ds_store-and-appledouble.html
categories:
  - Mac OS
tags:
  - Apple
  - Apple Double
  - AppleDouble
  - Desktop Services Store
  - DS_Store
  - mac
  - network drive
  - network share
  - network storage
  - networked drive

---

![thumb](/images/Apple_drive-e1432019517902-143x150.png)
How to find, remove and prevent the creating of the `.DS_Store` files and `.AppleDouble` directories on a networked drives.


**.DS_Store (short for Desktop Services Store)** - is a hidden file with a proprietary format created by OS X to store custom attributes of a folder such as the position of icons or the choice of a background image. By default, Finder creates a `.DS_Store` file in every folder that it accesses, even folders on remote systems (for example, folders shared over an SMB or AFP connection). The Microsoft equivalent for this file is `desktop.ini`.

**.AppleDouble** directories contain metadata relating to files. That allows the system to work with formats of disk (such as remote NFS, SMB, WebDAV directories, or local UFS volume) which does not support resource forks natively. The small binary files within the `.AppleDouble` directories have the same name as the actual files, and contain metadata about the file which cannot be stored inside the file itself, such as indexing information. Windows have similar metadata files called `Thumbs.db`.

`.DS_Store` and `.AppleDouble` are invisible to the average user, but if you are sharing with a Windows / UNIX PC or have hidden files shown in Finder then you will see them in every directory.


### Deleting all .DS_Store and .AppleDouble

The method described below will find and delete all `.DS_Store` files and `.AppleDouble` directories. This can help to avoid clutter on a networked drives.

**1.** Open Terminal.

**2.** Go to the needed directory, example:

```sh
cd your_folder
```

**3.** Execute this command:

```sh
find ./ -depth -name ".DS_Store" -exec rm {} \;
```

**4.** And then execute this command:

```sh
find ./ -depth -name ".AppleDouble" -exec rm -Rf {} \;
```

These commands search in every subdirectory, starting from the current directory.

Example, if you have such a directory structure:

<pre>
-- Photos
         `-- 2013-10-31 Halloween Photos
         |                              `-- .AppleDouble
         |-- 2013-10-32 Halloween Photos
         |                              `-- .AppleDouble
         |-- 2013-10-33 Halloween Photos
         |                              `-- .AppleDouble
         `-- 2013-10-34 Halloween Photos
                                        `-- .AppleDouble
                                        </pre>

Then do this:

```sh
cd Photos
find ./ -depth -name ".AppleDouble" -exec rm -Rf {} \;
```

**Note:** You can perform these steps on any UNIX systems (Mac, Linux etc.). 

**Note:** These steps do not prevent the Finder from creating .DS_Store files on the networked drives.


### Preventing creation of .DS_Store and .AppleDouble

You can also go a step further and prevent the OS X from creating the `.DS_Store` files on networked drives. For this, we will configure the OS X user account by use a `defaults write` command.

**1.** Open the Terminal app.

**2.** Execute this command:

```sh
defaults write com.apple.desktopservices DSDontWriteNetworkStores true
```

**3.** Either restart the computer or log out and back in to the user account.

If you want to prevent `.DS_Store` file creation for other users, then you need to perform the steps above on each user account on each Mac.

**Note:** This will affect the user’s interactions with SMB/CIFS, AFP, NFS and WebDAV servers.

**Note:** These steps do not prevent the Finder from creating `.DS_Store files` on the local volume and do not prevent previously existing `.DS_Store` files from being copied to the remote file server.

To stop the creation of `.AppleDouble` directories you need to edit your AFP service configuration (on a networked drive). There is usually a "No AppleDouble" or "Enable AppleDouble" configuration setting that needs to be set true (for the NO option) or set to false (for the Enable option).
