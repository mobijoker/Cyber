---
id: 580
lang: ru
ref: due-to-the-dos-attack-router-stops-working
title: Из-за DoS атак роутер перестаёт работать
date: 2015-05-15T09:48:14+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=580
permalink: /ru/linux/due-to-the-dos-attack-router-stops-working.html
switch_like_status:
  - 1
categories:
  - Error
  - Hacking
  - Linux
  - Электроника
tags:
  - asus
  - attack
  - DoS
  - dos-attack
  - log
  - logs
  - router
  - RT-N12
  - RT-N12E
  - RT-N12LX
  - shell

---

![thumb](/images/DoS-attack-and-wireless-router-300x300.png)
Что делать если, в логах ASUS роутера вы видите сообщения о DoS атаках, а затем ваш роутер перестаёт работать до следующей перезагрузки.


Недавно Я столкнулся с такой проблемой. Стал пропадать доступ в интернет и не получалось зайти в вэб-интерфейс роутера. Подключение к Wi-Fi сети было. После перезагрузки роутера всё исправлялось, но через некоторое время ситуация повторялась. А в логах бесконечно писалось о DoS-атаках.

	May 13 00:03:41 rlx-linux user.warn kernel: DoS: Port Scan Attack source=00.00.00.00 destination=00.00.00.00
	May 13 00:03:42 rlx-linux user.warn kernel: DoS: Port Scan Attack source=00.00.00.00 destination=00.00.00.00
	May 13 00:03:52 rlx-linux user.warn kernel: DoS: Port Scan Attack source=00.00.00.00 destination=00.00.00.00

Беспокоиться об этих атаках не нужно если роутер имеет защиту от них. Мой роутер имеет такую функцию. Но всё же стоит выяснить причину этих атак. Записи о DoS-атаке в логах не обязательно означают именно атаку, бывают и другие причины их появления.

Проблема же заключалась в другом. Так, как атаки были постоянными (каждую секунду) то, роутер не справлялся с записью информации о них в системные логи. Следовательно, если нет возможности устранить причину атак то, можно отключить логирование информации об атаках.

У меня роутер Asus RT-N12LX. Вэб-интерфейс роутера не имеет триггера для настройки или отключения логирования. В таком случае необходимо получить доступ к командной строке роутера. Самый безопасный способ это использовать SSH протокол, но можно использовать небезопасный Telnet так, как все роутеры ASUS содержат его. Если вэб-интерфейс вашего роутера не имеет триггера для включения Telnet, то вам необходимо прочитать эту статью: <a href="http://mycyberuniverse.com/linux/enable-telnet-on-the-asus-rt-n12e-lx-router.html" target="_blank">«Как включить Telnet сервер на роутере ASUS»</a>.


Сначало, найдём все переменные со словом `LOG` в NVRAM (Non Volatile Random Access Memory):

```
flash all | grep LOG
```

	DEF_SCRLOG_ENABLED=3
	DEF_REMOTELOG_ENABLED=0
	DEF_REMOTELOG_SERVER=""
	SCRLOG_ENABLED=3
	REMOTELOG_ENABLED=0
	REMOTELOG_SERVER=""
	Aborted

Нужная нам переменная это `SCRLOG_ENABLED`. Значение этой переменной `3`, это уровень логирования и мы можем его понизить до `2` или `1`. Если это не поможет, то можно установить значение `0` для полного отключения логирования.

Для понижения уровня логирования, введите это:

```
flash set SCRLOG_ENABLED 2
```

или это:

```
flash set SCRLOG_ENABLED 1
```

А для полного отключения логирования выполните это:

```
flash set SCRLOG_ENABLED 0
```

Теперь, необходимо перезагрузить роутер, для применения изменений:

```
reboot
```

Все предыдущие логи будут автоматически удалены после перезагрузки. Но если вам нужно немедленно удалить их (перед перезагрузкой) то введите это:

```
rm /var/log/messages*
```

А так вы можете увидеть логи:

```
ls /var/log/
```
