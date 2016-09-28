---
lang: ru
ref: backup-and-restore-complete-firefox-profile
title: 'Резервное копирование и восстановление профиля Firefox'
date: 2015-08-22T11:20:21+00:00
author: Arthur Gareginyan
layout: post
permalink: /ru/web/backup-and-restore-complete-firefox-profile.html
categories:
  - Web
tags:
  - add-ons
  - back up
  - backup
  - bookmarks
  - export
  - extensions
  - firefox
  - move
  - mozilla
  - profile
  - restore
  - transfer
  - дополнения
  - закладки
  - перенести
  - расширения

---

![thumb](/images/thumbnail/firefox_profile.png)
Как сделать резервную копию вашего профиля, восстановить его, или перенести профиль на новый компьютер. Для этого можно испольщовать расширения (“MozBackup” и “FEBE” популярный способ сделать это) или же можно сделать это легко вручную.


Mozilla Firefox хранит все персональные настройки, такие как закладки, пароли и расширения, в папке профиля на вашем компьютере, отдельно от программы Firefox.


### Резервное копирование

**Шаг 1.** Найдите и перейдите к папке Firefox «Profiles» (Профили).

На Mac OS X:
1) `~/Library/Application Support/Firefox/Profiles/`
2) `~/Library/Application Support/Mozilla/Firefox/Profiles/`

На Unix/Linux:
`/home/username/.mozilla/firefox/profiles/`

На Windows:
1) `C:/Documents and Settings/username/Application Data/Mozilla/Firefox/Profiles/`
2) `C:\Users\username\AppData\Roaming\Mozilla\Firefox\Profiles\`
3) `%APPDATA%\Mozilla\Firefox\Profiles\`

В зависимости от количества профилей которые вы имеете, вы увидите некоторое количество папок. Одна из них называется
какойто-текст.default. Это и есть папка профиля.

**Шаг 2.** Теперь можно копировать или архивировать профиль который хотите backup.


### Восстановление

**Шаг 1.** Установив Firefox, при первом запуске автоматически создастся "default" профиль Firefox, так-что не запускайте его.

**Шаг 2.** Перейдите в папку Firefox'а “Profiles“ (Профили).

**Шаг 3.** Вставьте the backed up папку профиля в новое место.

**Шаг 4.** Теперь можно запустить Firefox. Готово.
