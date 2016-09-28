---
lang: en
ref: convert-many-disk-image-formats-to-iso9660-from-terminal
title: Convert many disk image formats to ISO9660 from Terminal
date: 2015-02-28T16:57:17+00:00
author: Arthur Gareginyan
layout: post
permalink: /linux/convert-many-disk-image-formats-to-iso9660-from-terminal.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - B5I
  - BIN
  - CDI
  - convert
  - disk
  - format
  - image
  - ISO
  - ISO9660
  - MDF
  - MDX
  - NRG
  - PDI

---

![thumb](/images/thumbnail/disk.png)
There are many formats of disk images which is not possible to mount with standard Linux tools. But, with "Iat" tool, we can convert it to ISO format and then mount it with `mount` command.


Iat (Iso9660 Analyzer Tool) is a tool, by Salvatore Santagati, for detecting the structure of many types of CD-ROM image file formats, such as BIN, MDF, PDI, CDI, NRG, and B5I, and converting them into ISO (ISO-9660).


### Installation

It’s included in the Debian repositories, so installation is simple:

```sh
sudo apt-get install iat
```


### Using

It very easy to use:

```sh
iat input-image-file output-iso-file
```


EXAMPLES:

Convert MDX-image to ISO9660:

```sh
iat image.mdx image.iso
```

Convert NRG-image to ISO9660:

```sh
iat image.nrg image.iso
```

Convert BIN-image to ISO9660:

```sh
iat image.bin > image.iso
```

Write CD directly from MDF-image:

```sh
iat image.mdf | cdrecord
```

If output file name is not defined, then STDOUT will be used instead.

Then we can mount ISO image with standard Linux tools:

```sh
mount -o loop image.iso /mnt/disk
```
