---
lang: ru
ref: cap_sys_module-deprecated
title: CAP_SYS_MODULE (deprecated)
date: 2014-06-02
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/linux/cap_sys_module-deprecated.html
categories:
  - Debian/Ubuntu
  - Error
  - Linux
tags:
  - CAP_SYS_MODULE
  - deprecated
  - dist.conf
  - kernel
  - module
  - netdev-tun

---

![thumb](/images/thumbnail/error.png)
В новых ядрах начиная с 2.6 поддержка загрузки сетевых модулей при помощи `CAP_SYS_MODULE` признана устаревшей. И при попытке использовать виртуальные адаптеры в логах появляется сообщение:

<pre>
Loading kernel module for a network device with CAP_SYS_MODULE (deprecated). Use CAP_NET_ADMIN and alias netdev-tun instead
</pre>


Для того, чтобы исправить нужно в файл `/etc/modprobe.d/dist.conf` ( если файл не существует, то нужно создать ) добавить строку:

<pre>
alias netdev-tun tun
</pre>

В зависимости от имени интерфеса на которое ругается в сообщении.
