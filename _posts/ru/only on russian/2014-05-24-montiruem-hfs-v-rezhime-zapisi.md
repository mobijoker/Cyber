---
lang: ru
ref: montiruem-hfs-v-rezhime-zapisi
title: Монтируем HFS+ в режиме записи
date: 2014-05-24
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/linux/montiruem-hfs-v-rezhime-zapisi.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - debian
  - hfs
  - pi
  - raspberry
  - raspberrypi
  - ubuntu

---

![thumb]()
Mac OS форматирует накопители в файловую систему HFS+. В Debian, Ubuntu и Raspbian стандартные средства позволяют монтировать HFS+ разделы, но только в режиме `read-only` (только чтение).
Для возможности записи необходимо установить несколько пакетов.
 

```sh
sudo apt-get install hfsplus hfsutils hfsprogs
```

Создадим точку монтирования для раздела.

```sh
sudo mkdir /media/WD750
```

Подключим раздел на накопителе для проверки.

```sh
sudo mount -o force /dev/sda2 /media/WD750
```

Если раздел всёже монтируется только в `read-only` или он был неправильно извлечён или повреждён, тогда нужно воспользоваться программой `fsck.hfsplus`.

Перед этим отмонтируем накопитель:

```sh
sudo umount /media/WD750
```

Теперь запустим программу восстановления:

```sh
sudo fsck.hfsplus /dev/sda2
```

Вывод:

<pre>
** /dev/sda2
** Checking HFS Plus volume.
** Checking Extents Overflow file.
** Checking Catalog file.
** Checking Catalog hierarchy.
** Checking Extended Attributes file.
** Checking volume bitmap.
** Checking volume information.
** The volume WD750 appears to be OK.
</pre>

Если же вывод такой:

<pre>
** /dev/sda2
** Checking HFS Plus volume.
fsck_hfs: Volume is journaled.  No checking performed.
fsck_hfs: Use the -f option to force checking.
</pre>

Тогда нужно запустить программу с параметром `-f`:

```sh
sudo fsck.hfsplus -f /dev/sda2
```


### Автоматическое монтирование

Узнаем UUID накопителя одним из двух способов.


1) Смотрим в `/dev/disk/by-uuid`

```sh
ls -l /dev/disk/by-uuid
```

Вывод:

<pre>
lrwxrwxrwx 1 root root 10 Jan  1  1970 02cdd893-43cc-3811-9e82-d02afb65f2ad -> ../../sda2
</pre>


2) С помощью утилиты `blkid`

```sh
blkid /dev/sda2
```

Вывод:

<pre>
/dev/sda2: UUID="02cdd893-43cc-3811-9e82-d02afb65f2ad" LABEL="WD750" TYPE="hfsplus"
</pre>

Добавим запись в `fstab` для автоматического монтирования:

```sh
sudo nano /etc/fstab
```

<pre>
# EXTERNAL HDD
UUID="02cdd893-43cc-3811-9e82-d02afb65f2ad"     /media/WD750    hfsplus    defaults,force        0       0
</pre>

Проверим автомонтирование:

```sh
sudo mount -a
```

Теперь имеется возможность не только чтения с накопителя отформатированного в HFS+, но и записи, а также автоматическое монтирование.
