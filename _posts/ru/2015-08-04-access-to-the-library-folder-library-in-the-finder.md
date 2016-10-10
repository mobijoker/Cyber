---
lang: ru
ref: access-to-the-library-folder-library-in-the-finder
title: 'Доступ к папке Библиотеки (~/Library) в Finder'
date: 2015-08-04
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/mac-os/access-to-the-library-folder-library-in-the-finder.html
categories:
  - Mac OS
tags:
  - chflags
  - hidden
  - library
  - nohidden

---

![thumb](/images/access-to-the-library-folder-library-in-the-finder/Library.png)
С версии Mac OS X — 10.7 папка “Library” (Библиотеки) по умолчанию в Finder спрятана от пользователя.

 
### Способ №1

Эта возможность присутствует в OS X довольно давно. С помощью этого трюка можно быстро перейти в папку “Библиотеки”, при этом оставив её скрытой.

**1.** Откройте “Finder”.

**2.** Нажмите на вкладку “Go” (Переход) в строке меню.

**3.** Зажмите клавишу `Option` (`Alt`). После этого в списке для перехода к папкам появится и папка "Библиотеки":

<img class="aligncenter" src="/images/access-to-the-library-folder-library-in-the-finder/Library-2.png" alt="Library-2" width="571" height="415" />


### Способ №2

**1.** Откройте “Finder”.

**2.** Перейдите в домашнюю папку пользователя (для этого можно использовать сочетание клавиш `Command+Shift+H`).

**3.** Нажмите на вкладку “View” (Вид) в строке меню и выберите пункт “Show View Options” (Показать параметры вида).

<img class="aligncenter" src="/images/access-to-the-library-folder-library-in-the-finder/Library-3.png" alt="Library-3" width="650" height="372" />

**4.** Отметьте пункт “Show Library Folder” (Показывать папку «Библиотеки»).

После этого папка "Библиотеки" будет видна в вашей домашней папке.


### Способ №3

**1.** Откройте “Finder”.

**2.** Нажмите на вкладку “Go” (Переход) в строке меню и выберите пункт “Go to Folder…” (Переход к Папке). Или используйте сочетание клавиш `Cmd+Shift+G` (Переход к Папке).

<img class="aligncenter" src="/images/access-to-the-library-folder-library-in-the-finder/Library-4.png" alt="Library-2" width="524" height="234" />

**3.** Введите адрес каталога:

<pre>
~/Library
</pre>

Вы попадёте в каталог "Библиотеки".
 

### Способ №4

Этот способ использовался в OS X Lion и Mountain Lion, но так же работает в OS X Mavericks и Yosemite.

**1.** Запустите “Terminal” через “Spotlight” или “Launchpad” → “Utilities”

**2.** Введите следующую команду, чтобы показать спрятанную папку:

```sh
chflags nohidden ~/Library
```

Папка "Библиотеки" станет видимой.

Возврат к стандартным настройкам:

```sh
chflags hidden ~/Library
```
