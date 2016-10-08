---
lang: ru
ref: ustanovka-drayvera-nvidia-v-ubuntu-debian
title: Установка драйвера NVIDIA в Ubuntu/Debian
date: 2013-06-06
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
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

![thumb](/images/ustanovka-drayvera-nvidia-v-ubuntu-debian/nvidia.jpg)
Есть несколько способов установить проприетарный видео драйвер NVIDIA в Debian и производных от неё (например Ubuntu). В этой статье я опишу один из них. Такой способ установки не очень хорош так как входит в противоречие с пакетной системой Debian, что может привести к тому, что драйвер после обновления системы просто перестанет работать и тогда придётся его переустановить. Но не смотря на это иногда бывает проще установить драйвер именно таким способом.
 
**1.** Подключаем ветку **non-free**.

<a href="http://www.nvidia.ru/Download/index.aspx?lang=ru">Скачиваем драйвер</a> для своей видеокарты, в опциях поиска укажите **Linux 32-bit** или **Linux 64-bit** в зависимости от разрядности вашей системы.

**2.** Устанавливаем необходимые для последующей сборки пакеты:
 
<code>
sudo apt-get install linux-headers-`uname -r` binutils pkg-config build-essential xserver-xorg-dev
</code>

**3.** Переключаемся на виртуальную консоль, для этого нажмите сочетание клавишь **Ctrl+Alt+F1**.

**4.** Далее необходимо отключить оболочку, чтобы не получить вот такое сообщение:

<img src="/images/ustanovka-drayvera-nvidia-v-ubuntu-debian/stopx.png" />

Комманда остановки зависит от того какая оболочка установленна у вас.
Если версия Ubuntu 11.10 или выше (Unity):
 
```sh
sudo service lightdm stop
``` 


Если старая версия Ubuntu (Gnome):
 
```sh
sudo service gdm stop
``` 


Если оболочка "Gnome":
 
```sh
sudo service gdm stop
``` 

или:
 
```sh
sudo service gdm3 stop
``` 


Если оболочка "KDE":
 
```sh
sudo service kdm stop
``` 

**5.** Перейти в папку со скаченным драйвером. В моём случае файл лежит в домашней папке пользователя:
 
```sh
cd /home/user
``` 

**6.** Запускаем установщик (тот самый драйвер который скачали):
 
```sh
sudo sh ./NVIDIA-Linux-*.run
``` 

**7.** Отвечаем на вопросы установщика:

**8.** Перезагружаем компьютер:
 
```sh
reboot
``` 
