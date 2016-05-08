---
id: 606
lang: ru
ref: antivirus-on-a-linux-machine
title: Антивирус на Linux машине
date: 2015-05-31T04:44:30+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=606
permalink: /ru/linux/antivirus-on-a-linux-machine.html
categories:
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - antivirus
  - clam
  - clam antivirus
  - clamav
  - freshclam
  - malicious threats
  - malware
  - trojan
  - вирус
  - вредоносная программа
  - троян

---

![thumb](/images/clamav-trademark-300x244.png)
О том, как на Linux машине, используя программу ClamAV, обнаружить вредоносный код (трaояны, вирусы и вредоносные программы).
 

ClamAV (Clam AntiVirus) - это антивирусный движок c открытым исходным кодом для обнаружения троянов, вирусов, вредоносных программ и других вредоносных угроз на почтовых серверах, но его также можно использовать на десктопах.


### Установка

Он имеется в Debian репозитроии, поэтому установка проста:

```
sudo apt-get update
sudo apt-get install clamav
```


### Использование

Перед сканированием необходимо обновить базу данных сигнатур вирусов:

```
sudo freshclam
```

<pre>
ClamAV update process started at Tue May 19 17:02:33 2015
main.cvd is up to date (version: 55, sigs: 2424225, f-level: 60, builder: neo)
Downloading daily-20485.cdiff [100%]
daily.cld updated (version: 20485, sigs: 1392599, f-level: 63, builder: neo)
bytecode.cld is up to date (version: 256, sigs: 45, f-level: 63, builder: dgoddard)
Database updated (3816869 signatures) from db.local.clamav.net (IP: 198.148.78.4)
</pre>

Теперь можно начать сканирование любой директории (например `/home`) на наличие вирусов:

```
clamscan -r -i /home
```

* **-r** - Рекурсивное сканирование, т.е. сканирование в подкаталогах.
* **-i** - Показывать только инфицированные файлы.
* **/home** - Директория сканирования.

**Примечание:** Для сканирования всей системы (` / `) нужно запускать программу от имени рута (используя sudo).

**Примечание:** Эта команда только покажет инфицированные файлы, но не станет их очищать (лечить), отправлять на карантин или удалять.

У утилиты clamscan имеется множество дополнительных параметров для сканирования. Например:

* **--bell** - Звуковой сигнал при обнаружение инфекции.
* **--log** - Записать лог.
* **--max-dir-recursion** - Максимальная глубина поиска в директориях.
* **--exclude-dir** - Исключить директорию.
* **--copy** - Копирование инфицированных файлов в отдельную директорию.
* **--move** - Перемещение инфицированных файлов в отдельную директорию.
* **--remove** - Удаление инфицированных файлов.

О всех дополнительных параметрах можно узнать в `man`:

```
man clamscan
```

Пример использования дополнительных параметров:

```
sudo clamscan -ri --bell --max-dir-recursion=50 --move=/home/user/INFECTED/ --log=/var/log/clamav/clamav.log --exclude-dir=/mnt/storage/ /
```


### Автоматизация

Для автоматизации сканирования можно воспользоваться планировщиком задач Cron. Для этого нужно вписать несколько строк в файл `/etc/crontab`.

```
sudo nano /etc/crontab
```

<pre>
# ClamAV
0  3    * * *   root    /usr/bin/freshclam
20 3    * * *   root    /usr/bin/clamscan -r /
</pre>

Теперь сканирование будет происходить автоматически каждый день в 3 часа. Двадцатиминутный промежуток необходим для завершения работы `freshclam` (обновление базы данных).

**Примечание:** Установите любое удобное для вас время и замените строку `/usr/bin/clamscan -r /` на необходимую.


### Возможные находки

В результате сканирования могут обнаружиться такие "вирусы":

<pre>
PUA.Script.Packed-1 FOUND
PUA.Script.Packed-2 FOUND
</pre>

В действительности это не вирусы.

* PUA (Possibly Unwanted Applications) - Потенциально нежелательные приложения.
* Script.Packed - Скрипт упакован (архивирован).

Для того, чтобы отключить обнаружение PUA используйте дополнительный параметр:

<pre>
--detect-pua=no
</pre>

А для включения обнаружения PUA:

<pre>
--detect-pua=yes
</pre>

Пример:

```
sudo clamscan -r -i --detect-pua=yes / 
```


### Возможные ошибки

**ОШИБКА 1**

При обновлении базы данных сигнатур вирусов может выводится такое сообщение:

```
freshclam
```

<pre>
ERROR: Can't open /var/log/clamav/freshclam.log in append mode (check permissions!).
ERROR: Problem with internal logger (UpdateLogFile = /var/log/clamav/freshclam.log).
</pre>

Это происходит из-за того, что freshclam был запущен пользователем без определённых прав. Решается это запуском freshclam с помощью sudo:

```
sudo freshclam
```

**ОШИБКА 2**

При сканировании может выводится такое сообщение:

<pre>
LibClamAV Warning: fmap_readpage: pread fail: asked for 4085 bytes @ offset 11, got 0
LibClamAV Warning: fmap_readpage: pread fail: asked for 4091 bytes @ offset 5, got 0
LibClamAV Warning: fmap_readpage: pread fail: asked for 4094 bytes @ offset 2, got 0
LibClamAV Error: fmap_readpage: pread error: Input/output error
</pre>

Для того, чтобы это не происходило нужно исключить из сканирования несколько директорий, например так: 

```
sudo clamscan -ir --exclude-dir=^/sys --exclude-dir=^/dev --exclude-dir=^/proc /
```
