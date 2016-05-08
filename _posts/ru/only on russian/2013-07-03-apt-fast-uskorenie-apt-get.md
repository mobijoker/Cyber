---
id: 287
lang: ru
ref: apt-fast-uskorenie-apt-get
title: 'Apt-fast &#8211; ускорение apt-get'
date: 2013-07-03T23:49:36+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=287
permalink: /ru/linux/apt-fast-uskorenie-apt-get.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - apt-fast

---

![thumb]()
**Apt-fast** - это bash-скрипт созданный в 2008 году Мэттом Парнеллом (<a href="http://www.mattparnell.com">Matt Parnell</a>) для ускорения `apt-get` с помощью менеджера загрузок `axel` или `aria2`. Ускорение достигается за счёт загрузки в несколько потоков и использования нескольких источников (разных зеркал) для каждого файла. 
 
*[Официальная страница axel](http://axel.alioth.debian.org/)*

*[Официальная страница aria2](http://aria2.sourceforge.net/)*


**1)** Для того, чтобы использовать скрипт `apt-fast` сначала необходимо установить `axel` или `aria2`. Я ставлю `axel`.

Для `axel`:

```
sudo apt-get install axel
```

Для `aria2`:

```
sudo apt-get install aria2
```

**2)** Скачаем скрипт с сайта Мэтта Парнелла – <a href="http://www.mattparnell.com/linux/apt-fast/">http://www.mattparnell.com/linux/apt-fast/</a>. Для `axel` файл `apt-fast.sh`. А для `aria2` нужен файл `apt-fast_aria2c.sh` из поддиректории `apt-fast modded/`. Можно скачать скрипт с помощью консольной `wget`, не прибегая к GUI.

Для `axel`:

```
wget -U firefox http://www.mattparnell.com/linux/apt-fast/apt-fast.sh
```

Для `aria2`:

```
wget -U firefox http://www.mattparnell.com/linux/apt-fast/apt-fast%20modded/apt-fast_aria2c.sh
```

**3)** После скачивания, переименуем `apt-fast.sh` или `apt-fast_aria2c.sh` в `apt-fast` и перенесём в `/usr/bin/` для того, чтобы разрешить запуск скрипта как встроенной команды.

Для `axel`:

```
sudo mv apt-fast.sh /usr/bin/apt-fast
```

Для `aria2`:

```
sudo mv apt-fast_aria2c.sh /usr/bin/apt-fast
```

**4)** Дадим права на исполнение файлу apt-fast:

```
sudo chmod +x /usr/bin/apt-fast
```

**5)** Теперь проверим apt-fast в действии:

Обновим кэш пакетов:

```
sudo apt-fast update
```

И скачаем какой-нибудь пакет:

```
sudo apt-fast install “имя_пакета”
```

Теперь для установки любых пакетов в консоли мы будем использовать `apt-fast install “имя_пакета”` вместо `apt-get install “имя_пакета”`. Синтаксис команд у `apt-fast` тот же, что и у `apt-get`.
