---
id: 279
lang: ru
ref: avtozagruzka-v-linux
title: Автозагрузка в Linux
date: 2013-06-24T18:57:56+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=279
permalink: /ru/linux/avtozagruzka-v-linux.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - btsync
  - debian
  - init
  - init script
  - init.d
  - sysv-rc-conf
  - автозагрузка
  - скрипт инициализации
  - скрипт управления

---

![thumb](/images/thumbnail/sysv-rc-conf.png)
Любому демону нужен скрипт управления для того, чтобы его запускать, останавливать и т.д. Но не всегда в комплекте есть этот самый скрипт инициализации. Я опишу несколько примеров создания таких скриптов и способы управления ими.


Я буду показывать на примере сервиса для синхронизации файлов `btsync` (BitTorrent Sync).


### Управление автозагрузкой с помощью sysv-rc-conf

Для управления автозагрузкой я предпочитаю пользоваться программой `sysv-rc-conf`.

**1.** Устанавливаем `sysv-rc-conf` если ещё не установленна:

```sh
sudo apt-get install sysv-rc-conf
```

**2.** Запускаем `sysv-rc-conf`:

```sh
sudo sysv-rc-conf
```

**3.** Изменяем параметры на нужные:

```
btsync [][x][x][x][x][][][]
```

Находим в списке демон параметры автозагрузки которого необходимо изменить. Например `btsync` и отмечаем крестиками `2`,`3`,`4` и `5` уровни, что соотвествует параметрам автозапуска по дефолту. Если нужно отключить автозагрузку демона, тогда убираем все крестики. Отмечаем нажимая пробел. Настройка автоматически применяется. Для выхода нажимаем `q`.

Вот так просто решается вопрос управления параметрами автозагрузки демонов.


### Создание скрипта инициализации (простой)

**1.** Создаём файл (service init script) `/etc/init.d/btsync`:

```sh
sudo nano /etc/init.d/btsync
```

со следующим содержимым:

```sh
#!/bin/sh
### BEGIN INIT INFO
# Provides:     	btsync
# Required-Start:	$remote_fs $syslog
# Required-Stop: 	$remote_fs $syslog
# Default-Start: 	2 3 4 5
# Default-Stop:  	0 1 6
# Short-Description: Start btsync at boot time
# Description:   	Enable BitTorrent Sync service.
### END INIT INFO
 
/usr/local/bin/btsync --config ~/.btsync.conf
```

**2.** Дадим права на исполнение:

```sh
sudo chmod +x /etc/init.d/btsync
```

**3.** Обновляем ссылки на сценарии инициализации стиля `System-V`:

```sh
sudo update-rc.d btsync defaults
```

**4.** А теперь протестируем:

```sh
sudo service btsync start
```

**Примечание:** Такой init-скрипт умеет только запускать демон, но не останавливать. Этот способ подходит для тех случаев когда необходимо быстро прописать демон в автозагрузку. В таком случае остановить демон можно с помощью `killall <name>`.


### Создание скрипта инициализации (полноценный)

**1.** За основу берётся init-скрипт `/etc/init.d/skeleton`, по этому копируем его с новым именем соотвествующим имени демона, а точнее самого бинарника, а не его коммерческое название.

```sh
sudo cp /etc/init.d/skeleton /etc/init.d/btsync
```

**2.** Правим файл `/etc/init.d/btsync`:

```sh
sudo nano /etc/init.d/btsync
```

Нас интересует только эта часть скрипта:

```sh
#! /bin/sh
### BEGIN INIT INFO
# Provides:      	skeleton
# Required-Start:	$remote_fs $syslog
# Required-Stop: 	$remote_fs $syslog
# Default-Start: 	2 3 4 5
# Default-Stop:  	0 1 6
# Short-Description: Example initscript
# Description:   	This file should be used to construct scripts to be
#                	placed in /etc/init.d.
### END INIT INFO

# Author: Foo Bar <foobar@baz.org>
#
# Please remove the "Author" lines above and replace them
# with your own name if you copy and modify this script.

# Do NOT "set -e"

# PATH should only include /usr/* if it runs after the mountnfs.sh script
PATH=/sbin:/usr/sbin:/bin:/usr/bin
DESC="Description of the service"
NAME=daemonexecutablename
DAEMON=/usr/sbin/$NAME
DAEMON_ARGS="--options args"
PIDFILE=/var/run/$NAME.pid
SCRIPTNAME=/etc/init.d/$NAME
```

В которой мы должны подправить строки исходя из моих комментариев:

<pre>
# Provides:					(Название демона)
# Required-Start:	$remote_fs $syslog
# Required-Stop: 	$remote_fs $syslog
# Default-Start:					(Уровни загрузки)
# Default-Stop:					(Уровни остановки)
# Short-Description:				( Описание того, что делает скрипт)
# Description:					(Описание, что запускается)
# Author:						(Ваше имя, фамилия и email)
PATH=/sbin:/usr/sbin:/bin:/usr/bin	(Пути поиска бинарника)
DESC="Description of the service"	(Описание сервиса)
NAME=daemonexecutablename	(Имя бинарника)
DAEMON=/usr/sbin/$NAME		(Путь до демона)
DAEMON_ARGS="--options args"	(Параметры для запуска демона)
PIDFILE=/var/run/$NAME.pid		(Путь до pid-файла)
SCRIPTNAME=/etc/init.d/$NAME	(Имя скрипта в /etc/init.d/)
</pre>

**3.** Дадим права на исполнение:

```sh
sudo chmod +x /etc/init.d/btsync
```

**4.** Обновляем ссылки на сценарии инициализации стиля `System-V`:

```sh
sudo update-rc.d btsync defaults
```

**5.** А теперь протестируем:

```sh
sudo service btsync start
```

**Примечание:** В отличии от предыдущего скрипта этот имеет полную функциональность. Этот способ подходит для тех случаев когда необходим контроль над демоном. В таком случае управление демоном происходит с помощью `service <name> (start/stop/status)` или `/etc/init.d/<name> (start/stop/status)`.
