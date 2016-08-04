---
id: 273
lang: ru
ref: sinhronizatsiya-vremeni-ntp-2
title: 'Синхронизация времени &#8211; NTP'
date: 2013-06-23T17:47:58+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=273
permalink: /ru/linux/sinhronizatsiya-vremeni-ntp-2.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - ntp

---

![thumb](/images/clock.jpg)
**Network Time Protocol** (NTP) — сетевой протокол для синхронизации внутренних часов компьютера с использованием сетей с переменной латентностью.


### NTP-Client

**1.** Устанавливаем `ntp` клиент:

```sh
sudo apt-get install ntp ntpdate
```

**12.** Необходимо настроить `ntp` клиент для нашего региона. Нам нужен список серверов синхронизации времени. Сам список можно найти например на сайте <a href="http://www.pool.ntp.org/zone/@" target="_blank">www.pool.ntp.org/zone/@</a> который рекомендуется в конфигурационном файле NTP `/etc/ntp.conf`. Если вы из России, тогда можете использовать тот же список, что у меня в примере.

Открываем `/etc/ntp.conf`:

```sh
sudo nano /etc/ntp.conf
```

Находим такие строки:

	server 0.debian.pool.ntp.org iburst dynamic
	server 1.debian.pool.ntp.org iburst dynamic
	server 2.debian.pool.ntp.org iburst dynamic
	server 3.debian.pool.ntp.org iburst dynamic

И вместо них вписываем свой список серверов `ntp`:

	server 0.ru.pool.ntp.org iburst dynamic
	server 1.ru.pool.ntp.org iburst dynamic
	server 2.ru.pool.ntp.org iburst dynamic
	server 3.ru.pool.ntp.org iburst dynamic

**3.** Остановим `ntp`:

```sh
sudo service ntp stop
```

иначе при вводе следующей комманды мы получим такое сообщение:

	12 Jun 18:52:06 ntpdate[12097]: the NTP socket is in use, exiting

**4.** Сверимся с сервером при помощи `ntpdate`:

```sh
sudo ntpdate -q 0.ru.pool.ntp.org
```

На что получаем ответ:

```
server 93.180.7.2, stratum 2, offset 3,256055, delay 0.02960
server 188.134.15.192, stratum 2, offset 3,259242, delay 0.03915
server 62.76.96.4, stratum 2, offset 3.256370, delay 0.02861
server 93.180.6.3, stratum 2, offset 3.256370, delay 0.02885
13 Jun 04:13:40 ntpdate[32722]: adjust time server 62.76.96.4 offset 3.256370 sec
```

`Stratum 1` - Это сервер первого уровня (если `stratum 16`, значит сервер сам не синхронизирован).
`Offset` - Расхождение во времени с этим сервером в секундах.
`delay` - Задержка синхронизации в секундах.

Что значит то, что наши часы спешат на 3 секунды по сравнению с правильными. Такая разница кажется не значительной до смехоты но она очень значительна например для программ синхронизации файлов, которые могут даже просто отказаться от выпонения своих функций по синхронизации. Значит нам нужно синхронизировать наши часы с сервером точного времени.

**5.** Разово синхронизируем  часы при помощи того же `ntpdate`:

```sh
sudo ntpdate -bs 0.ru.pool.ntp.org
```

**6.** Снова сверимся для того, чтобы убедиться в том, что наши часы синхронизированны с сервером точного времени:

```sh
sudo ntpdate -q 0.ru.pool.ntp.org
```

	12 Jun 23:02:53 ntpdate[27338]: adjust time server 62.76.96.4 offset -0.000050 sec

Теперь часы идут точно!

**7.** Снова запустим `ntp`:

```sh
sudo service ntp start
```


### NTP-Server

Если у вас большая сеть и по политике безопасности сервер синхронизации времени ntp должен быть внутри корпоративной сети, тогда возложим эти функции на корпоративный сервер. Другими словами мы настроим один сервер синхронизироваться с внешним миром, а остальные сервера в нашей подсети будут синхронизироваться с этим.

**1.** Устанавливаем ntp-server:

```sh
sudo apt-get install ntp-server
```

**2.** На остальных компьютерах в сети указываем в роли сервера времени наш локальный ntp-сервер (вместо списка серверов).


### Разрешение доступа из локальной сети:

По умолчанию наш сервер `ntp` будет доступен всем хостам в Интернет. Параметр `restrict` в файле `/etc/ntp.conf` позволяет нам контролировать, какие машины могут обращаться к нашему серверу. Если мы хотим запретить всем машинам обращаться к нашему серверу ntp, тогда добавим следующую строку в файл `/etc/ntp.conf`:

```
restrict default ignore
```

Если мы хотим разрешить синхронизировать свои часы с нашим сервером только машинам в нашей сети, но запретить им настраивать сервер или быть равноправными участниками синхронизации времени, то вместо указанной добавим строчку:

```
restrict 10.0.0.0 mask 255.0.0.0 nomodify notrap
```

`/etc/ntp.conf` может содержать несколько директив `restrict`.

```
restrict 10.0.0.0 mask 255.0.0.0 noquery
```

**Примечание:**
Если наш ntp-сервер стоит за шлюзом, тогда надо на шлюзе разрешить входящий и исходящий трафик по 123 порту. 

Разрешение для входящего трафика:

```sh
sudo iptables -I INPUT -p udp --dport 123 -j ACCEPT
```

Разрешение для исходящего трафика:

```sh
sudo iptables -I OUTPUT -p udp --sport 123 -j ACCEPT
```


 
