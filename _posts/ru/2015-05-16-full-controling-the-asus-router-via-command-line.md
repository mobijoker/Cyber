---
lang: ru
ref: full-controling-the-asus-router-via-command-line
title: 'Полный контроль над роутером ASUS из командной строки'
date: 2015-05-16
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/linux/full-controling-the-asus-router-via-command-line.html
categories:
  - Hacking
  - Linux
  - Электроника
tags:
  - asus
  - cli
  - cmd
  - command line
  - commande
  - console
  - firmware
  - flash
  - original firmware
  - router
  - shell
  - telnet
  - консоль
  - маршрутизатор
  - рутер

---

![thumb](/images/thumbnail/Wireless-router.png)
Как получить полный контроль, над роутером ASUS с установленной оригинальной (заводской) прошивкой, через командную строку с помощью Telnet протокола доступа.


Для получения больших возможностей по настройке роутера многие тут-же прошивают роутер альтернативной прошивкой, такой как DDWRT, OpenWRT и другие. Но не всегда это оправдано. Вэб-интерфейс оригинальной прошивки может не содержать каких-то триггеров но в самой прошивки есть многие необходимые утилиты.

Значит, мы можем проделать все манипуляции над роутером с оригинальной (заводской) прошивкой, через командную строку с помощью Telnet протокола доступа.

Самый безопасный и мощный способ это использовать SSH протокол, но можно воспользоваться не безопасным Telnet так, как он имеется во всех роутерах ASUS.

Если вэб-интерфейс вашего роутера не имеет триггера для включения Telnet, то вам необходимо прочитать эту статью: <a href="http://mycyberuniverse.com/linux/enable-telnet-on-the-asus-rt-n12e-lx-router.html" target="_blank">«Как включить Telnet сервер на роутере ASUS»</a>.


### Получение доступа к командной строке

Прежде всего вам нужно подключиться к роутеру используя любой Telnet клиент, например PuTTY или консольный клиент.

Домен, IP-адрес, логин и пароль такие же как в вэб-интерфейсе роутера.

* **IP-адрес** — 192.168.1.1 (или тот который вы установили).
* **Домен** — router.asus.com (стандартный для ASUS роутеров)
* **Порт** — 23 (стандартный для Telnet протокола).
* **Имя пользователя (логин)** — “admin” (стандартный для ASUS роутеров).
* **Пароль** —  тот который вы установили (стандартный для ASUS роутеров - “admin”).

Для подключения с помощью консольного клиента:

**1.** Откройте терминал.

**2.** Подключитесь к роутеру по протоколу доступа Telnet:

```sh
telnet 192.168.1.1
```

**3.** Для авторизации используйте логин и пароль такие же как в вэб-интерфейсе роутера:

	Trying 192.168.1.1...
	Connected to 192.168.1.1.
	Escape character is '^]'.
	
	# |

Поздравляю, теперь вы в командной строке Linux роутер!


### В роутере

Теперь вы в командной строке Linux роутера ASUS.

В общем, Linux роутер очень похож на Debian но имеет некоторые особенности. Начну с общего.

Показать информацию о железе и прошивке роутера можно так:

```sh
cat /proc/version
```

	Linux version 2.6.30.9 (root@wireless-desktop) (gcc version 3.4.6-1.3.6) #4 Thu Jan 15 17:40:33 CST 2015

и так:

```sh
cat /proc/cpuinfo
```

	system type             : RTL8196C
	processor               : 0
	cpu model               : 52481
	BogoMIPS                : 389.12
	tlb_entries             : 32
	mips16 implemented      : yes

и так:

```sh
cat /etc/version
```

	RTL8196C v1.0 --   1  15 17:38:00 CST 2015
	The SDK version is: Realtek SDK v2.5-r
	Ethernet driver version is: -
	Wireless driver version is: -
	Fastpath source version is: -
	Feature support version is: -

Показать все примонтированные разделы, можно так:

```sh
mount
```

	rootfs on / type rootfs (rw)
	/dev/root on / type squashfs (ro,relatime)
	proc on /proc type proc (rw,relatime)
	ramfs on /var type ramfs (rw,relatime)

Как вы видите squashfs раздел примонтирован с параметром "ro" то есть только на чтение. Но, ramfs (/var) примонтирован с параметром "rw" то есть чтение и запись. Значит, мы можем создавать и удалять файлы в этой директории. Но после перезагрузки всё будет как раньше, а новые файлы будут удалены.

Все загрузочные скрипты находятся в директории "/etc/init.d/".

```sh
ls /etc/init.d/
```

	rcS
	rcS_16M

Это место находится на разделе подключённом в режиме только чтения, поэтому вы не можете добавлять свои скрипты сюда.

На роутере установлен BusyBox. BusyBox — это набор UNIX утилит командной строки, который используется в качестве основного интерфейса во встраиваемых операционных систем. В различных версиях и сборках он содержит различное количество утилит.

Для того, чтобы получить список команд, поддерживаемых данным экземпляром BusyBox, запустите его без каких-либо аргументов или используйте опцию "--list":

```sh
busybox
```

<pre>
BusyBox v1.13.4 (2015-01-15 17:36:18 CST) multi-call binary
Copyright (C) 1998-2008 Erik Andersen, Rob Landley, Denys Vlasenko
and others. Licensed under GPLv2.
See source distribution for full notice.

Usage: busybox [function] [arguments]...
   or: function [arguments]...

        BusyBox is a multi-call binary that combines many common Unix
        utilities into a single executable.  Most people will create a
        link to busybox for each function they wish to use and BusyBox
        will act like whatever it was invoked as!

Currently defined functions:
        arp, ash, bunzip2, bzcat, cat, cp, cut, date, echo, expr, false,
        free, grep, gzip, halt, head, hostname, ifconfig, init, ip, kill,
        killall, klogd, ln, ls, mkdir, mount, ping, poweroff, ps, reboot,
        renice, rm, route, sh, sleep, sync, syslogd, tail, telnetd, top,
        true, umount, vconfig, wc, zcip
</pre>

Для того, что бы узнать о том, что делают отдельные команды, используйте опцию "--help" в сочетании с этой командой:

```sh
busybox zcip --help
```

Но не все программы в прошивке являются частью BusyBox. Поэтому может потребоваться просмотреть список всех программ:

```sh
ls -l /bin
```

<pre>
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Get_BootLoaderVersion -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Get_FWVersion -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Get_FwReadyStatus -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Get_MacAddr_2G -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Get_PINCode -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Get_RegulationDomain -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Get_ResetButtonStatus -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Get_SWMode -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Get_WanLanStatus -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Get_WpsButtonStatus -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Set_AllLedOff -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Set_AllLedOn -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Set_MacAddr_2G -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Set_PINCode -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Set_RegulationDomain -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Set_RestoreDefault -> ate
lrwxrwxrwx    1 root     root            3 Jan 15 12:38 ATE_Set_StartATEMode -> ate
-rwxrwxrwx    1 root     root         8476 Jan 15 12:38 acltd
-rwxrwxrwx    1 root     root        13540 Jan 15 12:38 acs
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 arp -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 ash -> busybox
-rwxrwxrwx    1 root     root        21876 Jan 15 12:38 ate
-rwxrwxrwx    1 root     root         3324 Jan 15 12:38 atewatchdog
-rwxrwxrwx    1 root     root       177296 Jan 15 12:38 auth
-rwxrwxrwx    1 root     root        22836 Jan 15 12:38 brctl
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 bunzip2 -> busybox
-rwxrwxrwx    1 root     root       284072 Jan 15 12:38 busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 bzcat -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 cat -> busybox
-rwxrwxrwx    1 root     root           37 Jan 15 12:38 connect.sh
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 cp -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 cut -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 date -> busybox
-rwxrwxrwx    1 root     root         5096 Jan 15 12:38 ddns_inet
-rwxrwxrwx    1 root     root        12772 Jan 15 12:38 detectWAN
-rwxrwxrwx    1 root     root           28 Jan 15 12:38 disconnect.sh
-rwxrwxrwx    1 root     root        44260 Jan 15 12:38 dnrd
-rwxrwxrwx    1 root     root          207 Jan 15 12:38 dw
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 echo -> busybox
-rwxrwxrwx    1 root     root          123 Jan 15 12:38 ew
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 expr -> busybox
-rwxrwxrwx    1 root     root       110292 Jan 15 12:38 ez-ipupdate
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 false -> busybox
-rwxrwxrwx    1 root     root           29 Jan 15 12:38 firewall.sh
-rwxrwxrwx    1 root     root        84720 Jan 15 12:38 flash
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 free -> busybox
-rwxrwxrwx    1 root     root         7656 Jan 15 12:38 fwupgrade
-rwxrwxrwx    1 root     root           98 Jan 15 12:38 getmib
-rwxrwxrwx    1 root     root           98 Jan 15 12:38 getmib1
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 grep -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 gzip -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 halt -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 head -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 hostname -> busybox
-rwxrwxrwx    1 root     root       481996 Jan 15 12:38 httpd
-rwxrwxrwx    1 root     root         7592 Jan 15 12:38 httpdcheck
-rwxrwxrwx    1 root     root          104 Jan 15 12:38 ib
-rwxrwxrwx    1 root     root          104 Jan 15 12:38 ib1
-rwxrwxrwx    1 root     root          105 Jan 15 12:38 id1
-rwxrwxrwx    1 root     root          105 Jan 15 12:38 idd
-rwxrwxrwx    1 root     root          105 Jan 15 12:38 idd1
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 ifconfig -> busybox
-rwxrwxrwx    1 root     root        25264 Jan 15 12:38 igmpproxy
-rwxrwxrwx    1 root     root        16852 Jan 15 12:38 infosvr
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 init -> busybox
-rwxrwxrwx    1 root     root          116 Jan 15 12:38 init.sh
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 ip -> busybox
-rwxrwxrwx    1 root     root           72 Jan 15 12:38 ip_qos.sh
-rwxrwxrwx    1 root     root       321088 Jan 15 12:38 iptables
lrwxrwxrwx    1 root     root           13 Jan 15 12:38 iptables-restore -> /bin/iptables
-rwxrwxrwx    1 root     root          111 Jan 15 12:38 irf
-rwxrwxrwx    1 root     root          111 Jan 15 12:38 irf1
-rwxrwxrwx    1 root     root          104 Jan 15 12:38 iw
-rwxrwxrwx    1 root     root          104 Jan 15 12:38 iw1
-rwxrwxrwx    1 root     root        37424 Jan 15 12:38 iwcontrol
-rwxrwxrwx    1 root     root        27076 Jan 15 12:38 iwpriv
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 kill -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 killall -> busybox
-rwxrwxrwx    1 root     root          301 Jan 15 12:38 killsh.sh
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 klogd -> busybox
-rwxrwxrwx    1 root     root           27 Jan 15 12:38 l2tp.sh
-rwxrwxrwx    1 root     root       113968 Jan 15 12:38 l2tpd
-rwxrwxrwx    1 root     root        64352 Jan 15 12:38 lld2d
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 ln -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 ls -> busybox
-rwxrwxrwx    1 root     root        97348 Jan 15 12:38 miniigd
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 mkdir -> busybox
-rwxrwxrwx    1 root     root          182 Jan 15 12:38 mmd_cmdr
-rwxrwxrwx    1 root     root          196 Jan 15 12:38 mmd_cmdw
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 mount -> busybox
-rwxrwxrwx    1 root     root          589 Jan 15 12:38 mp.sh
-rwxrwxrwx    1 root     root        31004 Jan 15 12:38 networkmap
-rwxrwxrwx    1 root     root         9156 Jan 15 12:38 notify_service
-rwxrwxrwx    1 root     root         6912 Jan 15 12:38 ntp_inet
-rwxrwxrwx    1 root     root        25084 Jan 15 12:38 ntpclient
-rwxrwxrwx    1 root     root          115 Jan 15 12:38 ob
-rwxrwxrwx    1 root     root          115 Jan 15 12:38 ob1
-rwxrwxrwx    1 root     root          116 Jan 15 12:38 od
-rwxrwxrwx    1 root     root          116 Jan 15 12:38 od1
-rwxrwxrwx    1 root     root          122 Jan 15 12:38 orf
-rwxrwxrwx    1 root     root          122 Jan 15 12:38 orf1
-rwxrwxrwx    1 root     root          115 Jan 15 12:38 ow
-rwxrwxrwx    1 root     root          115 Jan 15 12:38 ow1
-rwxrwxrwx    1 root     root          184 Jan 15 12:38 phyr
-rwxrwxrwx    1 root     root          151 Jan 15 12:38 phyw
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 ping -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 poweroff -> busybox
-rwxrwxrwx    1 root     root         6520 Jan 15 12:38 ppp_inet
-rwxrwxrwx    1 root     root       276552 Jan 15 12:38 pppd
-rwxrwxrwx    1 root     root           30 Jan 15 12:38 pppoe.sh
-rwxrwxrwx    1 root     root           49 Jan 15 12:38 pppoe_conn_patch.sh
-rwxrwxrwx    1 root     root           87 Jan 15 12:38 pppoe_disc_patch.sh
-rwxrwxrwx    1 root     root        63784 Jan 15 12:38 pptp
-rwxrwxrwx    1 root     root           29 Jan 15 12:38 pptp.sh
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 ps -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 reboot -> busybox
-rwxrwxrwx    1 root     root        11699 Jan 15 12:38 reload
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 renice -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 rm -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 route -> busybox
-rwxrwxrwx    1 root     root        53887 Jan 15 12:38 routed
-rwxrwxrwx    1 root     root           48 Jan 15 12:38 rssi
-rwxrwxrwx    1 root     root           48 Jan 15 12:38 rssi1
-rwxrwxrwx    1 root     root          108 Jan 15 12:38 setmib
-rwxrwxrwx    1 root     root          108 Jan 15 12:38 setmib1
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 sh -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 sleep -> busybox
-rwxrwxrwx    1 root     root         2406 Jan 15 12:38 snmpd.sh
-rwxrwxrwx    1 root     root         8492 Jan 15 12:38 start_mac_clone
-rwxrwxrwx    1 root     root          656 Jan 15 12:38 startup.sh
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 sync -> busybox
-rwxrwxrwx    1 root     root       198664 Jan 15 12:38 sysconf
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 syslogd -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 tail -> busybox
-rwxrwxrwx    1 root     root       259828 Jan 15 12:38 tc
-rwxrwxrwx    1 root     root         7592 Jan 15 12:38 tcpcheck
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 telnetd -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 top -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 true -> busybox
lrwxrwxrwx    1 root     root            6 Jan 15 12:38 udhcpc -> udhcpd
-rwxrwxrwx    1 root     root        43595 Jan 15 12:38 udhcpd
-rwxrwxrwx    1 root     root        62408 Jan 15 12:38 udpxy
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 umount -> busybox
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 vconfig -> busybox
-rwxrwxrwx    1 root     root        38144 Jan 15 12:38 wanduck
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 wc -> busybox
-rwxrwxrwx    1 root     root           31 Jan 15 12:38 wlanapp.sh
-rwxrwxrwx    1 root     root       281752 Jan 15 12:38 wscd
lrwxrwxrwx    1 root     root            7 Jan 15 12:38 zcip -> busybox
-rwxrwxrwx    1 root     root          100 Jan 15 12:38 zcip.sh
</pre>

Если в списке вы видите что-то похожее на "[…] -> busybox" то эта программа является частью BusyBox.

Если нет нужной вам программы, то вы можете скачать её из интернета (или создать его путем кросс-компиляции) и положить в временный каталог («/tmp/»). Также вы можете скачать полную версию BusyBox с официального сайта (<a href="http://www.busybox.net" target="_blank">http://www.busybox.net</a>) и поместить его в временный каталог («/tmp/»). Но, как я писал выше, после перезагрузки всё будет как раньше и новые файлы будут удалены.

К примеру, в моём роутере, встроенный BusyBox (v1.13.4) не содержит редактор «vi» или «нано».


### NVRAM

А теперь про особенности о которых Я писал выше. Все настройки роутера (настройки изменяемые через веб-интерфейс, пользовательские настройки, загрузочные скрипты) хранятся в энергонезависимый памяти - NVRAM (Non Volatile Random Access Memory). Существует специальная команда для работы с этой памятью - "flash" и она уже установлена в оригинальную прошивку.

Его можно запустить без аргументов для того, чтобы увидеть все опции:

```sh
flash
```

<pre>
Usage: flash cmd
option:
cmd:
      default -- write all flash parameters from hard code.
      get [wlan interface-index] mib-name -- get a specific mib from flash
          memory.
      set [wlan interface-index] mib-name mib-value -- set a specific mib into
          flash memory.
      all -- dump all flash parameters.
      gethw hw-mib-name -- get a specific mib from flash
          memory.
      sethw hw-mib-name mib-value -- set a specific mib into
          flash memory.
      allhw -- dump all hw flash parameters.
      reset -- reset current setting to default.
      set_mib -- get mib from flash and set to wlan interface.
</pre>

Как вы можете видеть есть несколько опций. Аббревиатура «hw» означает - оборудование (железо).

Все настройки хранятся в переменных.

Показать все переменные::

```sh
flash all
```

<pre>
DEF_IP_ADDR=192.168.1.1
DEF_SUBNET_MASK=255.255.255.0
DEF_DEFAULT_GATEWAY=0.0.0.0
DEF_DHCP=2
DEF_DHCP_CLIENT_START=192.168.1.2
DEF_DHCP_CLIENT_END=192.168.1.254
DEF_DHCP_LEASE_TIME=0
DEF_DHCP_LEASE=86400
DEF_ELAN_MAC_ADDR=000000000000
DEF_DNS1=0.0.0.0
DEF_DNS2=0.0.0.0
DEF_DNS3=0.0.0.0
DEF_STP_ENABLED=0
DEF_DEVICE_NAME="RTL8196c"
....
</pre>

И многие другие переменные.

**Примечание:** Все переменные начинающиеся с префикса “DEF_” имеют значение по умолчанию (исходная конфигурация). Она включается при нажатии кнопки Reset на корпусе роутера или из веб-интерфейса роутера или с помощью команды «flash» в терминале.

**Примечание:** Не все из перечисленных переменных работают.Такие переменные как «SAMBA_ENABLED=0» не работают, из-за того, что Samba не установлен.

Для того, чтобы найти переменные с словом “NAME”, используйте команду «flash» совместно с «grep»:

```sh
flash all | grep "NAME"
```

<pre>
DEF_DEVICE_NAME="RTL8196c"
DEF_DOMAIN_NAME="ASUS"
DEF_SUPER_NAME="admin"
DEF_USER_NAME=""
DEF_PPP_USER_NAME=""
DEF_PPTP_USER_NAME=""
DEF_L2TP_USER_NAME=""
DEF_DDNS_DOMAIN_NAME=""
DEF_DDNS_SUGGEST_NAME=""
DEF_HOST_NAME=""
DEF_PPP_SERVICE_NAME=""
DEF_PPTPD_USERNAME=""
DEVICE_NAME="RT-N12LX"
DOMAIN_NAME="asus.loc"
SUPER_NAME="admin"
USER_NAME=""
PPP_USER_NAME="*****"
PPTP_USER_NAME=""
L2TP_USER_NAME=""
DDNS_DOMAIN_NAME=""
DDNS_SUGGEST_NAME=""
HOST_NAME=""
PPP_SERVICE_NAME=""
PPTPD_USERNAME=""
Aborted
</pre>

**Примечание:** Имена всех переменных записываются в верхнем регистре.

Показать значение определенной переменной (например, имя администратора):

```sh
flash get SUPER_NAME
```

	SUPER_NAME="admin"

Установить новое значение переменной (например, имя администратора):

```sh
flash set SUPER_NAME superadmin
```

Теперь у вас есть новое имя администратора (логин), а это повышает безопасность.

Но для того, что бы изменения вступили в силу необходимо перезагрузить роутер:

```sh
reboot
```

Если необходимо вернуть все заводские параметры (сброс к изначальным настройкам):

```sh
flash default
```


**P.S.**
Если вы не нашли в этой статье нужную вам информацию, то вы сможете найти её в комментариях ниже.
