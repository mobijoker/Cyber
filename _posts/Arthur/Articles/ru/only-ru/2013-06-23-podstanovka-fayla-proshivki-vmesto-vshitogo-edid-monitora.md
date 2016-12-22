---
lang: ru
ref: podstanovka-fayla-proshivki-vmesto-vshitogo-edid-monitora
title: Подстановка файла прошивки вместо вшитого EDID монитора
date: 2013-06-23
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/linux/podstanovka-fayla-proshivki-vmesto-vshitogo-edid-monitora.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - edid

---

![thumb](/images/thumbnail/EDID.png)
В том случае если вшитый EDID дисплея испорчен, а такое случается часто, можно подсунуть системе файл прошивки. Конечно, в том случае если прошивка имеется. Поэтому я всегда на всякий случай делаю дампы (резервные копии) прошивок всех моих мониторов, так как уже был случай когда мне пришлось разбирать дисплей ноутбука для того, чтобы узнать серийный номер по которому предстояло долго искать на форумах ту самую прошивку. В этой статье я расскажу о том как снять дамп прошивки EDID дисплея и как подсунуть его системе на базе Debian и производных (Ubuntu) с видеокартой «NVIDIA» и проприетарным драйвером «nvidia».


Из wiki:
<blockquote>
<b>«Extended Display Identification Data (EDID)</b> — это стандарт формата данных VESA, который содержит базовую информацию о мониторе и его возможностях, включая информацию о производителе, максимальном размере изображения, цветовых характеристиках, заводских предустановленных таймингах, границах частотного диапазона, а также строках, содержащих название монитора и серийный номер.»
</blockquote>


### Создание дампа прошивки

Опишу два примера создания дампа прошивки EDID дисплея.

**Шаг 1.** Первый пример подходит всем, в не зависимости от установленной видео-карты и используемого драйвера.

Устанавливаем пакет `read-edid`:

```sh
sudo apt-get install read-edid
```

Считаем EDID дисплея:

```sh
sudo get-edid | parse-edid
```

> **Примечание:**
`get-edid` - считывает EDID, а `read-edid` преобразует его в читабельный вид.

Считать EDID и записать его в файл:

```sh
sudo get-edid > edid.bin
```

Прочитать файл прошивки EDID:

```sh
sudo parse-edid < edid.bin
```

> **Примечание:**
Если возникает такая ошибка:

<pre>
Error: output block unchanged
parse-edid: IO error reading EDID
</pre>

тогда попробуйте ещё раз. Если эта ошибка возникает постоянно тогда это значит, что ваш EDID монитора скорее всего повреждён и делать дамп бессмысленно.

**Шаг 2.** Второй способ сделать дамп прошивки для тех у кого видеокарта «NVIDIA» и используется проприетарный драйвер «nvidia».

В «nvidia-settings» есть кнопка «Adquire EDID», которая сохраняет EDID дисплея в двоичном или текстовом формате. Вот так просто.


### Подстановка дампа прошивки EDID в xorg.conf

Сначало узнаем как именуется наш монитор:

```sh
cat /etc/X11/xorg.conf | grep ConnectedMonitor
```

Вы должны увидеть такой вывод:

<pre>
Option "ConnectedMonitor" "DFP-0"
</pre>

Где `DFP-0` и есть необходимый нам номер.

Дальше поправим `xorg.conf` для чтения EDID из файла прошивки. Откроем для редактирования `xorg.conf`:

```sh
sudo nano /etc/X11/xorg.conf
```

Добавим следующую информацию в «Section "Device"»:

<pre> 
 Option         "ConnectedMonitor" "DFP-0"
 Option         "CustomEDID" "DFP-0:/etc/X11/edid.bin"
 Option         "IgnoreEDID" "false"
 Option         "UseEDID" "true"
</pre>
 
Измените `DFP-#` номер на тот который узнали прежде. Вместо `/etc/X11/edid.bin` укажите на свой файл прошивки. Он не обязательно должен лежать в `/etc/X11/`. В результате «Section "Device"» должен выглядеть примерно так:

<pre>
Section "Device"
  Identifier     "nvidia"
  Driver         "nvidia"
  Option         "DynamicTwinView" "false"
  Option         "NoFlip" "false"
  Option         "NoLogo" "true"
  Option         "ModeValidation" "NoVesaModes, NoXServerModes"
  Option         "ConnectedMonitor" "DFP-0"
  Option         "CustomEDID" "DFP-0:/etc/X11/edid.bin"
  Option         "IgnoreEDID" "false"
  Option         "UseEDID" "true"
 EndSection
</pre>

После перезагрузки система считает EDID дисплея из нашего дампа прошивки, а не из дисплея.
