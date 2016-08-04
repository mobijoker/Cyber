---
lang: ru
ref: otklyuchenie-modulya-nouveau
title: Отключение модуля nouveau
date: 2013-06-09T00:13:44+00:00
author: Arthur Gareginyan
layout: post
permalink: /ru/linux/otklyuchenie-modulya-nouveau.html
categories:
  - Debian/Ubuntu
  - Linux
tags:
  - nouveau

---

![thumb](/images/nvidia-linux.png)
Бывает появляется необходимость отключить модуль `nouveau`, например если необходимо использовать универсальный модуль `vesafb` или перед установкой проприетарного видео-драйвера NVIDIA.


Из <a href="http://ru.wikipedia.org/wiki/Nouveau" target="_blank">Wiki</a>:

<blockquote>"nouveau ([nuvo]) — проект по созданию свободных драйверов видеокарт компании nVIDIA с поддержкой ускорения вывода трёхмерной графики. Изначально основан на распространяемом по свободной лицензии, но нечитаемом драйвере «nv» 2D-графики от nVIDIA."</blockquote>

Если установщик `nvidia-installer` обнаружит активный драйвер Nouveau, он предложит создать файл настроек `modprobe` для отключения Nouveau. После чего потребуется перезагрузить компьютер и снова запустить `nvidia-installer`. Но мы пойдём инным путём и создадим такой файл настроек `modprobe` вручную.

Можно отредактировать уже имеющийся файл `/etc/modprobe.d/blacklist.conf` но тогда при обновление системы файл может быть обновлён и изменения будут потеряны.

Поэтому вместо редактирования уже имеющегося файла создадим новый файл, например `/etc/modprobe.d/disable-nouveau.conf` и впишем в него две строки.

Вне зависимости от того, создаете ли вы новый файл или редактируете имеющийся, в него должны быть добавлены следующие строки:


	blacklist nouveau
	options nouveau modeset=0


Первая строка запрещает модулю Nouveau уровня ядра автоматически загружаться при загрузке операционной системы. Она не предотвратит загрузку модуля по требованию, как и загрузку модуля сервером Х-интерфейса. Вторая строка запретит драйверу Nouveau осуществлять операции смены видеорежима через ядро.

Просто копируйте команды ниже, вставьте их в терминале (для тех кто вдруг ещё не знает, это тот который открывается после одновременного нажатия **CTRL+ALT+T**) и нажмите **ENTER**, а когда попросит ввести пароль сделайте это.
 
```sh
sudo echo “blacklist nouveau” &amp;gt; /etc/modprobe.d/disable-nouveau.conf
sudo echo “options nouveau modeset=0” &amp;gt;&amp;gt; /etc/modprobe.d/disable-nouveau.conf
reboot
``` 

Готово!
