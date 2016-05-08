---
id: 12
lang: ru
ref: dobavlyaem-polnotsennyiy-port-kinect-v-xbox360-fat
title: Добавляем порт Kinect в XBox360 FAT
date: 2013-05-11T23:35:47+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=12
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

![thumb]()
Статья о том, как добавить специальный порт для сенсора Kinect в игровой консоли XBox360 FAT.


У меня есть игровая консоль XBox360 (FAT) и Kinect сенсор (модель для XBox360 FAT). Так-как в FAT версии нет порта Kinect а в SLIM он есть то для FAT версии продаётся комплект Kinect с внешним блоком питания и переходником на USB.

<img class="wp-image-620 size-medium" src="/images/Kinect-for-FAT-300x224.jpeg" alt="Kinect for FAT" width="300" height="224" />
<caption>Kinect sensor for XBox360 FAT</caption>

Или можно приобрести блок питания с переходником отдельно от Kinect.

<img class="wp-image-621 size-medium" src="/images/Kinect-power-supply-e1434218521514-300x214.jpg" alt="Kinect power supply" width="300" height="214" />
<caption>Kinect sensor power supply</caption>

Мне постоянно мешал внешний блок питания и переходник от Kinect и тогда Я решил модифицировать XBox360 добавив порт Kinect как в SLIM версии консоли для того, чтобы избавиться от лишних проводов.


### Питание

Во-первых Kinect'у необходимо питание. Оригинальный блок питания для Kinect выдаёт `12В` и `1.08А`. Можно использовать штатный блок питания XBox в котором имеется 12-и вольтовая шина достаточной мощности, а точнее аж `12,1А`. Есть несколько мест с которых можно получить необходимое питание. Я предпочёл подключится к месту у самого входа питания на материнскую плату так, как в таком случае все компоненты материнской платы будут работать в штатном режиме. Нагрузка будет только на блоке питания.

Теперь нужно найти распиновку разъёма питания XBox360 и подключиться к нему на материнской плате.

<img class="size-medium wp-image-465" src="/images/360female-289x300.png" alt="Power connector" width="289" height="300" />
<caption>Power connector of XBox360</caption>

<img class="size-medium wp-image-469" src="/images/PWRConnector-251x300.jpg" alt="Power connector" width="251" height="300" />
<caption>Power connector of XBox360</caption>

Нужные контакты:

* `Жёлтый` - 12В.
* `Чёрный` - Масса.


### Данные

Данные Kinect передаёт по специальному кабелю. Для того, чтобы подключить его к USB-порту необходим переходник с USB на Kinect-port.

<img class="wp-image-467 size-medium" src="/images/kinect-extension-cable-e1434218471965-300x135.jpg" alt="Kinect sensor extension cable" width="300" height="135" />
<caption>Kinect sensor extension cable</caption>

**Примечание:** Если у вас нет переходника USB-Kinect то его можно сделать самостоятельно из подручных деталей и материалов. Инструкции есть в сети.

Внутри консоли нам нужен USB-порт для того, чтобы подключить к нему переходник с USB-Kinect. Я не нашёл свободный (не распаянный) USB-порт на материнской плате и поэтому решил использовать один из внешних USB-портов припаяв к нему USB-female порт изнутри. При этом будет нельзя подключать другие устройства (флешки, джойстики) к этому порту с наружи так, как теперь он будет занят изнутри. Я выбрал один из двух портов на передней панели потому, что мне достаточно только одного из них.


### Модификация

**Шаг 1.** Сначало нужно разобрать XBox и достать материнскую плату так. Разборка не сложна и инструкций в сети много.

<a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1487.jpg" target="_blank"><img class="aligncenter wp-image-633 size-medium" src="/images/IMG_1487-225x300.jpg" alt="IMG_1487" width="225" height="300" /></a>

<a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1499.jpg" target="_blank"><img class="alignnone wp-image-634 size-medium" src="/images/IMG_1499-300x225.jpg" alt="IMG_1499" width="300" height="225" /></a> <a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1500.jpg" target="_blank"><img class="alignnone wp-image-632 size-medium" src="/images/IMG_1500-300x225.jpg" alt="IMG_1500" width="300" height="225" /></a>

**Шаг 2.** Припаеваем провода питания к материнской плате.

<a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1502.jpg" target="_blank"><img class=" size-medium wp-image-628 alignnone" src="/images/IMG_1502-300x225.jpg" alt="IMG_1502" width="300" height="225" /></a> <a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1498.jpg" target="_blank"><img class="alignnone wp-image-635 size-medium" src="/images/IMG_1498-300x225.jpg" alt="IMG_1498" width="300" height="225" /></a>

**Шаг 3.** Припаеваем USB-female порт к одному из двух USB портов на передней панели.

<a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1507.jpg" target="_blank"><img class=" size-medium wp-image-627 alignnone" src="/images/IMG_1507-300x225.jpg" alt="IMG_1507" width="300" height="225" /></a> <a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1501.jpg" target="_blank"><img class=" size-medium wp-image-631 alignnone" src="/images/IMG_1501-300x225.jpg" alt="IMG_1501" width="300" height="225" /></a>

**Шаг 4.** Закрепляем новый порт (внутренний USB) на корпусе.

<a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1496.jpg" target="_blank"><img class="aligncenter wp-image-637 size-medium" src="/images/IMG_1496-300x225.jpg" alt="IMG_1496" width="300" height="225" /></a>

**Шаг 5.** Подключаем переходник USB-Kinect к внутреннему USB-порту (только-что установленный USB-female порт ) и укладываем кабель так, чтобы он не мешал.

<a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1493.jpg" target="_blank"><img class="aligncenter wp-image-638 size-medium" src="/images/IMG_1493-300x225.jpg" alt="IMG_1493" width="300" height="225" /></a>

**Шаг 6.** Новый разъём (другая сторона только-что установленного переходника USB-Kinect) устанавливаем и закрепляем термопластичным клеем на любое свободное место на задней панели XBox. Соответственно придётся вырезать отверстие под новый разъём. Мне больше понравилось место за наклейкой над разъёмом питания.

<a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1494.jpg" target="_blank"><img class="alignleft wp-image-639 size-medium" src="/images/IMG_1494-300x225.jpg" alt="IMG_1494" width="300" height="225" /></a>  <a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1495.jpg" target="_blank"><img class="alignnone wp-image-636 size-medium" src="/images/IMG_1495-300x225.jpg" alt="IMG_1495" width="300" height="225" /></a>

**Примечание:** На этом месте был один из пластиковых замков (защёлка) корпуса который пришлось отрезать. Но после сборки корпуса стыки остались прежними. Корпус плотно закрыт после удаления одного из 7-и замков!

**Шаг 7.** Собираем XBox в обратном порядке.

В итоге XBox360 FAT имеет порт Kinect как и SLIM версия консоли.

<a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1489.jpg" target="_blank"><img class="alignnone wp-image-630 size-medium" src="/images/IMG_1489-225x300.jpg" alt="IMG_1489" width="225" height="300" /></a> <a href="http://mycyberuniverse.com/wp-content/uploads/IMG_1490.jpg" target="_blank"><img class="alignnone wp-image-629 size-medium" src="/images/IMG_1490-300x225.jpg" alt="IMG_1490" width="300" height="225" /></a>

И на наклейке остался текст с характеристиками блока питания.

Я использую XBox с такой модификацией уже примерно год. Блок питания XBox не греется.
