---
id: 432
lang: ru
ref: perezapusk-setevogo-interfeysa-pri-nedostupnosti-hosta
title: Перезапуск сетевого интерфейса при недоступности хоста
date: 2014-07-19T18:25:21+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=432
permalink: /ru/linux/perezapusk-setevogo-interfeysa-pri-nedostupnosti-hosta.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
  - Мои программы
tags:
  - interface
  - pi
  - raspberry
  - raspberrypi
  - shell
  - wifi

---

![thumb](/images/bash.png)
Мой Raspberry Pi подключен к локальной сети по WiFi с помощью USB WiFi адаптера «ASUS USB-N10» и при сбоях в сети (например когда рутер зависает или перезагружается) RPi не переподключается к WiFi сети. Чтобы исправить эту ситуацию Я написал маленький сценарий на «Shell» проверяющий доступность сети пингуя рутер и перезапускающий интерфейс `wlan0`. После записи в `cron` сценарий будет проверять сеть каждую минуту.


* **Name:** ifdown_net.sh
* **Description:** Ping host and restart interface if host is down
* **Language:** Shell

```
#!/bin/sh
#=============================================================#
# Name:         If Down Net                                   #
# Description:  Checking the net by ping and restart          #
#               interface if is need                          #
# Version:      ver 1.0                                       #
# Data:         10.7.2014                                     #
# Author:       Arthur (Berserkr) Gareginyan                  #
# Author URI:   http://mycyberuniverse.com/author.html        #
# Email:        arthurgareginyan@gmail.com                    #
# License:      GNU General Public License, version 3 (GPLv3) #
# License URI:  http://www.gnu.org/licenses/gpl-3.0.html      #
#=============================================================#

#                       USAGE:
#               chmod +x ifdown_net.sh
#     Add folowing line to the end of the /etc/crontab :
#     */1  *    * * *   root    /home/user/ifdown_net.sh

# The host to test by ping. You can use IP or domain name.
HOST="192.168.1.1"

# The device wich need to reload
DEVICE='wlan0'

########################## BEGIN ##############################
# Check the availability of a host
ping -c 3 $HOST >/dev/null 2>&1

# Restart interface if host is down
if [ $? -ne 0 ] ; then
        ifup $DEVICE ; 
fi

exit 0
```

В коде нужно исправить переменные `HOST` и `DEVICE` на необходимые.

Дадим права на исполнение:

```
chmod +x ifdown_net.sh
```

И сделаем запись в `cron` для автоматического запуска скрипта каждую минуту:

```
sudo nano /etc/crontab
```

<pre>
# Test interface and reload if need
*/1  *    * * *   root    /home/user/ifdown_net.sh
</pre>

Если хочется запускать не каждую минуту, а например каждые 5 минут, тогда нужно исправить `1` на `5`.

<br/>
{% assign url = "https://github.com/ArthurGareginyan/restart-interface-if-host-down" %}{% include button-github.html %}
