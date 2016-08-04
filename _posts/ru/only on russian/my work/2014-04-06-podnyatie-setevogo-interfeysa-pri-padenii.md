---
lang: ru
ref: podnyatie-setevogo-interfeysa-pri-padenii
title: Поднятие сетевого интерфейса при падении
date: 2014-04-06T08:01:32+00:00
author: Arthur Gareginyan
layout: post
permalink: /ru/linux/podnyatie-setevogo-interfeysa-pri-padenii.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
  - Мои программы
tags:
  - broker
  - client
  - debian
  - gogo
  - gogo6
  - gogoc
  - interface
  - ipv6
  - tun
  - tunel
  - ubuntu

---

![thumb](/images/bash.png)
Для получения адреса IPv6 на одном из серверов я пользуюсь услугами тунельного брокера <a href="http://gogo6.com" title="gogo6.com" target="_blank">gogo6.com</a>. Для подключения к брокеру используется программа `gogoc` (gogo client), которая поднимает виртуальный интерфейс `tun` для создания тунеля. Но, время от времени, этот интерфейс падает, что делает сервер более не доступным по IPv6 адресу.

Причину падения интерфейса я определил но решил ,что оптимальным решением будет перезапускать интерфейс в случае падения. Для этого я написал сценарий на "Shell" проверяющий нужный интерфейс на существование, а в случае отсутствия перезапускающий программу `gogoc`. И ещё неообходима запись в `cron` для запуска этого сценария по расписанию.

Код написан под перезапуск gogoc но может быть легко переделан под другие нужды.


* **Name:** IfDownTun.sh
* **Description:** Check and start interface tun if it down
* **Language:** Shell

```bash
#!/bin/sh
#################################################################
#   Name: 	 	 IfDownTun		   								#
#   Description: Check and start iinterface tun if it down 		#
#   Author: 	 Arthur Gareginyan aka Berserkr    				#
#   Author URI:  http://mycyberuniverse.com/author.html			#
#   Email: 	 	 arthurgareginyan@gmail.com        				#
#   License:     GNU General Public License, version 3 (GPLv3)  #
#   License URI: http://www.gnu.org/licenses/gpl-3.0.html		#
#   Usage: 		 chmod +x IfDownTun.sh							#
#   Run:   		 ./IfDownTun.sh									#
#################################################################

# The interface to test
DEVICE='tun'
#TEST_IFACE=`/sbin/ip link show dev $DEVICE >/dev/null 2>/dev/null`

# Check the availability of an interfac
/sbin/ip link show dev $DEVICE >/dev/null 2>/dev/null

# Raising of the interface tun if not raised
if [ "$?" = "1" ] ; then
        if [ ! -f /tmp/iface_tun.error ] ; then
        	echo "$(date '+%F(%H:%M)') iface tun DOWN" >> /var/log/iface_tun.log
        	touch /tmp/iface_tun.error
        fi
        killall gogoc ;
        service gogoc start ;
        sleep 10

        # Again checking and recording info in /var/log/iface_tun.log when success
        /sbin/ip link show dev $DEVICE >/dev/null 2>/dev/null
        if [ "$?" = "0" ] ; then
                echo "$(date '+%F(%H:%M)') iface tun UP" >> /var/log/iface_tun.log
                rm /tmp/iface_tun.error
                exit 0
        fi
fi

exit 0

```

Необходимо дать права на исполнение:

```sh
chmod +x IfDownTun.sh
```

И сделать запись в `cron` для автоматического запуска скрипта по расписанию:

```sh
sudo nano /etc/crontab
```

<pre>
# Test if iface tun is down
*/3 *   * * *   root    /home/IfDownTun.sh
</pre>

Сценарий также пишет логи в `/var/log/iface_tun.log`. В таком формате:
<pre>
2014-03-18(02:51) iface tun DOWN
2014-03-19(16:45) iface tun UP
2014-03-19(16:48) iface tun DOWN
2014-03-20(16:21) iface tun UP
2014-03-20(22:57) iface tun DOWN
2014-03-20(22:57) iface tun UP
2014-03-21(14:51) iface tun DOWN
2014-03-21(14:51) iface tun UP
</pre>

<br/>
{% assign url = "https://github.com/ArthurGareginyan/If-interface-tun-down" %}{% include button-github.html %}
