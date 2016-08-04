---
lang: en
ref: access-to-the-library-folder-library-in-the-finder
title: Access to the Library folder (~/Library) in the Finder
date: 2015-08-04T18:55:10+00:00
author: Arthur Gareginyan
layout: post
permalink: /mac-os/access-to-the-library-folder-library-in-the-finder.html
categories:
  - Mac OS
tags:
  - chflags
  - hidden
  - library
  - nohidden

---

![thumb](/images/Library.png)
From version of Mac OS X  —  10.7, the folder "Library", in the Finder, by default is hidden from the user.


### Method №1

This feature is present in OS X for quite a long time. Using this trick you can quickly go to a folder "Library", while leaving her hidden.

**1.** Open the “Finder”.

**2.** Click on the tab “Go” in the menu bar.

**3.** Hold down the Option key (`Alt`). Then, "Library" folder will appear in the list:

<img class="aligncenter size-full" src="/images/Library-2.png" alt="Library-2" width="571" height="415" />


### Method №2

**1.** Open the “Finder”.

**2.** Go to the home directory of the user (to do this, you can use the keyboard shortcut `Command+Shift+H`).

**3.** Click on the tab “View” in the menu bar and select “Show View Options”.

<img class="aligncenter size-full" src="/images/Library-3.png" alt="Library-3" width="650" height="372" />

**4.** Select “Show Library Folder”.

Then you will see the "Library" folder in your home folder.


### Method №3

**1.** Open the “Finder”.

**2.** Click on the tab “Go” in the menu bar and select “Go to Folder…”. Or use the keyboard shortcut `Cmd+Shift+G`.

<img class="aligncenter size-full" src="/images/Library-4.png" alt="Library-2" width="524" height="234" />

**3.** Enter the address of the directory:

<pre>
~/Library
</pre>

You'll find the directory "Library".


### Method №4

This method was used in OS X Lion and Mountain Lion, but also works in OS X Mavericks and Yosemite.

**1.** Run the "Terminal" through the “Spotlight” or “Launchpad” -&gt; “Utilities”

**2.** Type the following command to show the hidden folder:

```sh
chflags nohidden ~/Library
```

Folder "Library" will be visible.

Return to the default settings:

```sh
chflags hidden ~/Library
```
