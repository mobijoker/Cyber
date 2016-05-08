---
id: 264
lang: ru
ref: byistro-zashifrovat-fayl-v-linux
title: Быстро зашифровать файл в Linux
date: 2013-06-22T05:25:05+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=264
permalink: /ru/linux/byistro-zashifrovat-fayl-v-linux.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - debian
  - контейнер

---

![thumb]()
Есть множество способов зашифровать файл в Linux. Многие из них требуют ввода множества параметров. Я же опишу один из самых простых и быстрых способов сделать это. В этом нам поможет пакет `ccrypt`. 


На официальной странице <a href="http://ccrypt.sourceforge.net/">http://ccrypt.sourceforge.net/</a> имеются прекомпилированные и собранные пакеты на разные системы:
 
Precompiled distributions:

* Linux (32 bit)
* Linux (64 bit)
* Windows 95/98/2000/NT
* Sun Solaris (Sparc)
* Mac OS X (universal)
* AIX
* Linux for Alpha
* Linux for AMD64
* Sun Solaris (i386)
* FreeBSD
* NetBSD
* HP-UX
* Linux for Sparc
* Linux for ARM
* Linux for Power PC

Packages:

* Debian Package (i386)
* Redhat Source RPM
* Redhat Binary RPM (i386)
* Solaris Package (Sparc)
* Solaris Package (i386)
* OS/2 Package
* SuSE Source RPM
* SuSE Binary RPM (i586)
* OpenBSD Package (i386)
* FreeBSD Package (i386)

Также он имеется в стандартных репозиториях Debian. 
Установка осуществляется стандартным образом:
 
```
sudo apt-get install ccrypt
``` 

Для того, что бы зашифровать какой либо файл используется `ccrypt` или `ccrypt -e` или `ccencrypt`. По сути это всё одна команда. Разницы в них нет, так что выбираем тот вариант который больше нравится (проще запомнить). Параметр `-e` указывает программе на то, что файл требуется именно зашифровать но `ccrypt` без указания параметров и так зашифровывает, по этому указывать не обязательно. Например, зашифруем файл `file`:

```
ccrypt -e file
```

Программа спросит пароль и подтверждение пароля:

```
Enter encryption key: 
Enter encryption key: (repeat)
```

После чего выдаст файл контейнер `file.cpt` вместо исходного файла, который и будет содержать зашифрованную копию файла `file`. 

Для прочтения зашифрованного текстового файла можно использовать команду `ccrypt -c` или `ccat`, тем самым уменьшая вероятность оставить следы от файла.

```
ccrypt -c file
Enter decryption key:
Hello world!
```

Исходя из выше сказанного понятно, что для дешифровки нужно использовать `ccrypt -d` или `ccdecrypt`, кому как нравится.

```
ccrypt -d file.cpt
Enter decryption key:
```

И тогда вместо зашифрованного контейнера появится наш файл. 

В качестве алгоритма шифрования используется шифр `Rijndael`, выбранный в США в качестве национального стандарта "AES" (см. <a href="http://www.nist.gov/aes" target="_blank">http://www.nist.gov/aes</a>). Так что наши данные будут в безопасности.

*Из Wiki:*

<blockquote>
<p dir="ltr">Advanced Encryption Standard (AES), также известный как Rijndael (произносится [rɛindaːl] (Рейндол) ) —симметричный алгоритм блочного шифрования (размер блока 128 бит, ключ 128/192/256 бит), принятый в качестве стандарта шифрования правительством США по результатам конкурса AES. Этот алгоритм хорошо проанализирован и сейчас широко используется, как это было с его предшественником DES. Национальный институт стандартов и технологий США (англ. National Institute of Standards and Technology, NIST) опубликовал спецификацию AES 26 ноября2001 года после пятилетнего периода, в ходе которого были созданы и оценены 15 кандидатур. 26 мая 2002 года AES был объявлен стандартом шифрования. По состоянию на 2009 год AES является одним из самых распространённых алгоритмов симметричного шифрования. Поддержка AES (и только его) введена фирмой Intel в семейство процессоров x86 начиная с Intel Core i7-980X Extreme Edition, а затем на процессорах Sandy Bridge.</p>
</blockquote>
