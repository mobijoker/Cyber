---
id: 97
lang: ru
ref: ustanovka-drayvera-nvidia-v-ubuntu-debian
title: Установка драйвера NVIDIA в Ubuntu/Debian
date: 2013-06-06T01:38:35+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=97
permalink: /ru/linux/ustanovka-drayvera-nvidia-v-ubuntu-debian.html
categories:
  - Debian/Ubuntu
  - Linux
tags:
  - debian
  - gnome
  - nvidia
  - ubuntu
  - unity
  - драйвер
  - консоль

---

![thumb]()
Есть несколько способов установить проприетарный видео драйвер NVIDIA в Debian и производных от неё (например Ubuntu). В этой статье я опишу один из них. Такой способ установки не очень хорош так как входит в противоречие с пакетной системой Debian, что может привести к тому, что драйвер после обновления системы просто перестанет работать и тогда придётся его переустановить. Но не смотря на это иногда бывает проще установить драйвер именно таким способом.
 
**1.** Подключаем ветку **non-free**.

<a href="http://www.nvidia.ru/Download/index.aspx?lang=ru">Скачиваем драйвер</a> для своей видеокарты, в опциях поиска укажите **Linux 32-bit** или **Linux 64-bit** в зависимости от разрядности вашей системы.

**2.** Устанавливаем необходимые для последующей сборки пакеты:
 
<code>
sudo apt-get install linux-headers-`uname -r` binutils pkg-config build-essential xserver-xorg-dev
</code>

**3.** Переключаемся на виртуальную консоль, для этого нажмите сочетание клавишь **Ctrl+Alt+F1**.

**4.** Далее необходимо отключить оболочку, чтобы не получить вот такое сообщение:

<a href="http://mycyberuniverse.com/wp-content/uploads/stopx.png"><img src="/images/stopx.png" /></a>

Комманда остановки зависит от того какая оболочка установленна у вас.
Если версия Ubuntu 11.10 или выше (Unity):
 
```
sudo service lightdm stop
``` 


Если старая версия Ubuntu (Gnome):
 
```
sudo service gdm stop
``` 


Если оболочка "Gnome":
 
```
sudo service gdm stop
``` 

или:
 
```
sudo service gdm3 stop
``` 


Если оболочка "KDE":
 
```
sudo service kdm stop
``` 

**5.** Перейти в папку со скаченным драйвером. В моём случае файл лежит в домашней папке пользователя:
 
```
cd /home/user
``` 

**6.** Запускаем установщик (тот самый драйвер который скачали):
 
```
sudo sh ./NVIDIA-Linux-*.run
``` 

**7.** Отвечаем на вопросы установщика:

**8.** Перезагружаем компьютер:
 
```
reboot
``` 
