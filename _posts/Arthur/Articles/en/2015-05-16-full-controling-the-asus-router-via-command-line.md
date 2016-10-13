---
lang: en
ref: full-controling-the-asus-router-via-command-line
title: Full controlling the ASUS router via command line
date: 2015-05-16
author: Arthur Gareginyan
layout: post
permalink: /linux/full-controling-the-asus-router-via-command-line.html
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
How to full controlling the ASUS router with original firmware via a command line by the Telnet access protocol.


For get more opportunities to configure router, many people flash they routers by alternative firmware such as OpenWRT, DDWRT and others. But this is not always justified. The web interface of the original firmware may not contain certain triggers but the firmware contain many of the necessary tools.

So, we can try to implement all necessary manipulations over the router from the original firmware via a command line by the Telnet access protocol.

The most secure and powerful way is using the SSH protocol, but you have to use the insecure Telnet as that's all ASUS routers ship with it by default.

If the web-interface of your ASUS router don't have a trigger to enable a Telnet access protocol then read this article: <a href="http://mycyberuniverse.com/linux/enable-telnet-on-the-asus-rt-n12e-lx-router.html" target="_blank">«How to enable the Telnet server on the ASUS router»</a>.


### Getting command line access

First of all, you need to connect to your router by use any Telnet client, for example the PuTTY or a command line client.

Domain, IP-address, username and password is same as in the web interface of the router.

* **IP-address** — `192.168.1.1` (or whatever you set).
* **Domain** — `router.asus.com` (default for ASUS routers)
* **Port** — `23` (default for Telnet protocol).
* **Username** — `admin` (default for ASUS routers).
* **Password** is whatever you set (default for ASUS routers is `admin`).

To use a command line client:

**1.** Open Terminal App.

**2.** Connect to the router via Telnet access protocol by enter this command:

```sh
telnet 192.168.1.1
```
**3.** Login using username and password the same as in the web admin panel of the router.

<pre>
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^]'.

# |
</pre>

Congratulations, now you in the command line of the Linux router!


### Inside the router

Now we in the command line of the Linux router ASUS.

In general, the Linux router is very similar to Debian but has some its features. I'll start with the general.

To show info about hardware and firmware of your router you can do by this way:

```sh
cat /proc/version
```

<pre>
Linux version 2.6.30.9 (root@wireless-desktop) (gcc version 3.4.6-1.3.6) #4 Thu Jan 15 17:40:33 CST 2015
</pre>

and this way:

```sh
cat /proc/cpuinfo
```

<pre>
system type             : RTL8196C
processor               : 0
cpu model               : 52481
BogoMIPS                : 389.12
tlb_entries             : 32
mips16 implemented      : yes
</pre>

and this way:

```sh
cat /etc/version
```

<pre>
RTL8196C v1.0 --   1  15 17:38:00 CST 2015
The SDK version is: Realtek SDK v2.5-r
Ethernet driver version is: -
Wireless driver version is: -
Fastpath source version is: -
Feature support version is: -
</pre>

To show all mounted volumes, run this:

```sh
mount
```

<pre>
rootfs on / type rootfs (rw)
/dev/root on / type squashfs (ro,relatime)
proc on /proc type proc (rw,relatime)
ramfs on /var type ramfs (rw,relatime)
</pre>

How you see the squashfs volume is mounted in `ro` i.e. reed only. But the ramfs (`/var`) is `rw` i.e. read and write. So we can create and delete files in this directory. But after the reboot everything will be like before and new files will be deleted. 

All initialization scripts are placed in the directory `/etc/init.d/`.

```sh
ls /etc/init.d/
```

<pre>
rcS
rcS_16M
</pre>

This place is read only, so you can't add your own script's to this place.

On the router installed BusyBox. BusyBox — is a set of UNIX command line tools, is used as the primary interface in embedded operating systems. In different versions and builds it contain a different number of tools.

To get a list of the commands supported by this instance of BusyBox, run it without any arguments, or use the `--list` option:

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

To see what an individual command does, use the `--help` option to that command:

```sh
busybox zcip --help
```

But not all programs in the firmware is a part of the BusyBox. So you may need to see a list of all programs:

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

If, in the list, you see something like `[…] -> busybox`, then this program is a part of the BusyBox.

If you don't see the program that you need then you can download it from internet (or create it by cross compiling) and put in the temp directory (`/tmp/`). Also you can download full BusyBox from official website (<a href="http://www.busybox.net" target="_blank">http://www.busybox.net</a>) and put it in the temp directory (`/tmp/`). But, how I write above, after the reboot everything will be like before and new files will be deleted.

For example, in my router built-in BusyBox (v1.13.4) doesn't contain editor `vi` or `nano`.


### NVRAM

And now about the its features of which I wrote above. All the settings of the router (settings editable through a web interface, user settings, startup scripts) are stored in nonvolatile memory - NVRAM (Non Volatile Random Access Memory). There is a special command to work with this memory - `flash`. The `flash` is already installed in original firmware.

Run it without any arguments to see all options:

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

As you can see there is a few options. The abbreviation `hw` means - hardware.

All the settings are stored in the variables.

To show all variables:

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

And many more variables.

**Note:** All variables which started with `DEF_` prefix is have a default value (original configuration). It’s enabled via pushing Reset button on the router or from the web interface of the router or via command `flash` in the terminal.

**Note:** Not everyone of the listed variables are working. Variables like a `SAMBA_ENABLED=0` is not working, because of the Samba is not installed.

To find variables with word `NAME`, use command `flash` together with the `grep`:

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

**Note:** The names of all variables are written in top register.

To show the value of a specific variable (for example, name of administrator):

```sh
flash get SUPER_NAME
```

<pre>
SUPER_NAME="admin"
</pre>

To set the new value to a variable (for example, name of administrator):

```sh
flash set SUPER_NAME superadmin
```

Now, you have the new name of admin (login) and it improves the security.

But, for the changes to take effect you must reboot your router:

```sh
reboot
```

If you need to return the original settings (reset to original configuraton):

```sh
flash default
```

<br>

**P.S.**
If you don't find in this article the desired information then you may find it in the comments bellow.
