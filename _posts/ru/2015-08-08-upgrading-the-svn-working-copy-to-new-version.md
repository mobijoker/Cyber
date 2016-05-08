---
id: 676
lang: ru
ref: upgrading-the-svn-working-copy-to-new-version
title: 'Обновление рабочей копии SVN до новой версии'
date: 2015-08-08T23:33:39+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=676
permalink: /ru/linux/upgrading-the-svn-working-copy-to-new-version.html
categories:
  - Debian/Ubuntu
  - Linux
  - Mac OS
  - Raspberry Pi
tags:
  - checkout
  - E155036
  - repository
  - svn
  - svn error
  - upgrade
  - working copy is too old

---

![thumb](/images/SubVersion-120x120.png)
Сегодня, на моём компьютере, Я обновил Subversion с версии 1.6 до версии 1.7. Subversion версии 1.7 имеет структуру репозитория and требует обновления всех существующих рабочих копий.


Если мы попытаемся использовать Subversion 1.7 на рабочей копии созданной более старой версией Subversion, то мы увидим следующее сообщение об ошибке:

```
svn status
```

<pre>
svn: E155036: Please see the 'svn upgrade' command
svn: E155036: Working copy '/home/user/project' is too old (format 10, created by Subversion 1.6)
</pre>

Нам нужно использовать команду `svn upgrade` для обновления рабочей копии до последнего формата метаданных, поддерживаемого новой версией Subversion.

```
svn upgrade [PATH TO PROJECT]
```

<pre>
Upgraded '.'
Upgraded 'A'
Upgraded 'A/B'
Upgraded 'A/B/E'
</pre>

Теперь моя рабочая копия обновлена!

**Примечание:** Команду `svn upgrade` необходимо применить к каждой рабочей копии.

**Примечание:** После обновления Subversion до версии 1.7, вы не сможете вернуться к Subversion 1.6. И обновленные рабочие копии будут непригодны для использования в более старых версиях Subversion.

**Примечание:** Команда `svn upgrade` может занять некоторое время, поэтому для некоторых пользователей может быть более практичным просто создать новую рабочую копию (checkout).
