---
lang: en
ref: find-and-remove-dublicate-files-from-the-terminal
title: Find and remove duplicate files from the terminal
date: 2015-02-17T23:28:39+00:00
author: Arthur Gareginyan
layout: post
permalink: /linux/find-and-remove-dublicate-files-from-the-terminal.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - duplicate
  - fdupes

---

![thumb](/images/duplicates.png)
If you have a lot of media files (photo, music etc), then most likely you also have a lot of duplicate files. In this article I'll show you how to find and remove duplicate files, from the terminal, by using `fdupes` utility.


`fdupes` — is a program written by Adrian Lopez to scan directories for duplicate files, with the option to display a list and automatic removal of duplicates. It first compares file sizes, partial MD5 signatures, full MD5 signatures, and then performs a byte-by-byte comparison for verification.

With the `fdupes` you can remove duplicate files very easily.

But first you need to install `fdupes`:

```
sudo apt-get install fdupes
```

To search a directory for duplicate files, simply run the following command:

```
fdupes ./
```

<pre>
Progress [5539/39061] 14%
</pre>

The command will search the directory for any duplicate files and show the progress-bar, and then show the results.

Also, you can redirect the results of serching to a text file:

```
fdupes -r ./ > duplicates.txt
```

The fdupes can do more with options like:

* **r** - search recursively (in subdirectories).
* **d** - delete duplicates.
* **N** - used together with `d`, preserve the first file in each set of duplicates and delete the others without prompting the user.

#### Examples:

To recursively search the directory and delete duplicates:

```
fdupes -r -d catalog/
```

You will need to manually select a file for deleting in each set of duplicates.

Or you can run following command for automatically delete the duplicate files:

```
fdupes -r -d -N catalog/
```

The results of running the utility:

<pre>
[+] ./catalog/file.jpg
[-] ./catalog/file-1.jpg
[-] ./catalog/file-2.jpg
</pre>

Marked as plus is the kepted file and marked as minus is the deleted files.

Also note that the two following commands do the same things:

```
fdupes -r -d -N ./
```

and:

```
fdupes -rdN ./
```
