---
lang: ru
ref: otklyuchenie-rezhima-energosberezheniya-wifi-adaptera
title: Отключение режима энергосбережения WiFi адаптера
date: 2014-05-31
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/linux/otklyuchenie-rezhima-energosberezheniya-wifi-adaptera.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - 8192cu
  - adapter
  - asus
  - management
  - mode
  - n10
  - pi
  - power
  - raspberry
  - realtek
  - rpi
  - saving
  - sleep
  - usb-n10
  - wifi
  - режим
  - спящий
  - энергосбережение

---

![thumb](/images/thumbnail/WiFi.png)
После некоторого времени простоя Raspberry Pi, USB-WiFi адаптер переходит в режим энергосбережения (saving mode) и к RPi больше нельзя подключиться по SSH.

Дано:

1. Raspberry Pi B ревизии.
2. WiFi адаптер “ASUS USB-N10” с чипом `Realtek 8192cu` (используется во многих адаптерах).
 

Проблема состоит в том, что чип `8192cu` имеет функцию управления питанием (power management) включенную по умолчанию. Так ли это можно проверить, выполнив команду:

```sh
cat /sys/module/8192cu/parameters/rtw_power_mgnt
```

* **0** - Управление питанием отключено.
* **1** - Минимальные настройки энергосбережения.
* **2** - Максимальные настройки энергосбережения.

Чтобы отключить функцию управления питанием, нужно создать новый файл:

```sh
sudo nano /etc/modprobe.d/8192cu.conf
```

Вписать туда эти строки:

<pre>
# Disable power management
options 8192cu rtw_power_mgnt=0
</pre>

И перезагрузить RPi:

```sh
sudo reboot
```

После перезагрузки проверим статус энергосбережения:

```sh
cat /sys/module/8192cu/parameters/rtw_power_mgnt
```

Должен быть `0`.

> **Примечание:** Решение подходит и к другим Linux.
