---
lang: ru
ref: dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat
title: Добавляем порт Kinect в XBox360 FAT
date: 2013-05-11
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/electronics/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat.html
categories:
  - Электроника
tags:
  - kinect
  - kinect power supply
  - xbox
  - xbox 360
  - xbox 360 power supply pinout
  - xbox fat
  - xbox power supply pinout
  - xbox360
  - xbox360 Fat
  - xbox360 power supply pinout

---

![thumb](/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/kinect-top-hard-01-top.jpg)
Статья о том, как добавить специальный порт для сенсора Kinect в игровой консоли XBox360 FAT.

&nbsp;
&nbsp;
&nbsp;

У меня есть игровая консоль XBox360 (FAT) и Kinect сенсор (модель для XBox360 FAT). Так-как в FAT версии нет порта Kinect а в SLIM он есть то для FAT версии продаётся комплект Kinect с внешним блоком питания и переходником на USB.

<img src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/Kinect-for-FAT.jpg" alt="Kinect for FAT" />
<caption>Kinect sensor for XBox360 FAT</caption>

Или можно приобрести блок питания с переходником отдельно от Kinect.

<img src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/Kinect-power-supply.jpg" alt="Kinect power supply" />
<caption>Kinect sensor power supply</caption>

Мне постоянно мешал внешний блок питания и переходник от Kinect и тогда Я решил модифицировать XBox360 добавив порт Kinect как в SLIM версии консоли для того, чтобы избавиться от лишних проводов.


### Питание

Во-первых Kinect'у необходимо питание. Оригинальный блок питания для Kinect выдаёт `12В` и `1.08А`. Можно использовать штатный блок питания XBox в котором имеется 12-и вольтовая шина достаточной мощности, а точнее аж `12,1А`. Есть несколько мест с которых можно получить необходимое питание. Я предпочёл подключится к месту у самого входа питания на материнскую плату так, как в таком случае все компоненты материнской платы будут работать в штатном режиме. Нагрузка будет только на блоке питания.

Теперь нужно найти распиновку разъёма питания XBox360 и подключиться к нему на материнской плате.

<img src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/360female.png" alt="Power connector of XBox360" />
<img src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/PWRConnector.jpg" alt="Power connector of XBox360" />

Нужные контакты:

* `Жёлтый` - 12В.
* `Чёрный` - Масса.


### Данные

Данные Kinect передаёт по специальному кабелю. Для того, чтобы подключить его к USB-порту необходим переходник с USB на Kinect-port.

<img src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/kinect-extension-cable.jpg" alt="Kinect sensor extension cable" />
<caption>Kinect sensor extension cable</caption>

**Примечание:** Если у вас нет переходника USB-Kinect то его можно сделать самостоятельно из подручных деталей и материалов. Инструкции есть в сети.

Внутри консоли нам нужен USB-порт для того, чтобы подключить к нему переходник с USB-Kinect. Я не нашёл свободный (не распаянный) USB-порт на материнской плате и поэтому решил использовать один из внешних USB-портов припаяв к нему USB-female порт изнутри. При этом будет нельзя подключать другие устройства (флешки, джойстики) к этому порту с наружи так, как теперь он будет занят изнутри. Я выбрал один из двух портов на передней панели потому, что мне достаточно только одного из них.


### Модификация

**Шаг 1.** Сначало нужно разобрать XBox и достать материнскую плату так. Разборка не сложна и инструкций в сети много.

<img class="aligncenter" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1487.jpg" />
<img class="alignnone" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1499.jpg" />
<img class="alignnone" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1500.jpg" />

**Шаг 2.** Припаеваем провода питания к материнской плате.

<img class="alignnone" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1502.jpg" />
<img class="alignnone" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1498.jpg" />

**Шаг 3.** Припаеваем USB-female порт к одному из двух USB портов на передней панели.

<img class="alignnone" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1507.jpg" />
<img class="alignnone" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1501.jpg" />

**Шаг 4.** Закрепляем новый порт (внутренний USB) на корпусе.

<img class="aligncenter" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1496.jpg" />

**Шаг 5.** Подключаем переходник USB-Kinect к внутреннему USB-порту (только-что установленный USB-female порт ) и укладываем кабель так, чтобы он не мешал.

<img class="aligncenter" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1493.jpg" />

**Шаг 6.** Новый разъём (другая сторона только-что установленного переходника USB-Kinect) устанавливаем и закрепляем термопластичным клеем на любое свободное место на задней панели XBox. Соответственно придётся вырезать отверстие под новый разъём. Мне больше понравилось место за наклейкой над разъёмом питания.

<img class="alignleft" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1494.jpg" />
<img class="alignnone" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1495.jpg" />

**Примечание:** На этом месте был один из пластиковых замков (защёлка) корпуса который пришлось отрезать. Но после сборки корпуса стыки остались прежними. Корпус плотно закрыт после удаления одного из 7-и замков!

**Шаг 7.** Собираем XBox в обратном порядке.

В итоге XBox360 FAT имеет порт Kinect как и SLIM версия консоли.

<img class="alignnone" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1489.jpg" />
<img class="alignnone" src="/images/dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat/IMG_1490.jpg" />

И на наклейке остался текст с характеристиками блока питания.

Я использую XBox с такой модификацией уже примерно год. Блок питания XBox не греется.
