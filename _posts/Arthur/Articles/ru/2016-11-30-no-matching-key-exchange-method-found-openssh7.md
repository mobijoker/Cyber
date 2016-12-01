---
title: 'Как исправить: В OpenSSH 7.0 не найден соответствующий метод обмена ключами '
ref: no-matching-key-exchange-method-found-openssh7
permalink: /ru/error/no-matching-key-exchange-method-found-openssh7.html
author: Arthur Gareginyan
translator: Arthur Gareginyan
lang: ru
layout: post
categories:
  - error
tags:
  - fix
  - how to fix
  - error
  - issue
  - problem
  - ошибка
  - проблема
  - как исправить
  - как починить
  - ssh
  - openssh7
  - openssh 7
  - openssh 7.0
  - diffie-hellman-group1-sha1
  - unable to negotiate with
  - no matching key exchange method found
  - Logjam attack
  - Logjam атака
  - key exchange algorithm

---

![thumb](/images/thumbnail/error.png)
После обновления SSH до новой версии (7.0), при попытке подсоеленится к моему серверу при помощи SSH, Я получаю следующее сообщение:
<pre>
Unable to negotiate with 192.168.1.1 port 22: no matching key exchange method found.
Their offer: diffie-hellman-group1-sha1
</pre>


<br>

### Чем вызвана эта проблема

В OpenSSH 7.0 алгоритм ключа `diffie-hellman-group1-sha1` по умолчанию выключен, потому что он слаб и в теории подвержен Logjam атаке. Смотрите страницу [www.openssh.com/legacy.html](http://www.openssh.com/legacy.html) для получения дополнительной информации.

Если клиент и сервер не могут договориться о взаимном наборе параметров, то соединение не будет установлено. OpenSSH (7.0 и выше) покажет такое сообщение об ошибке:

<pre>
Unable to negotiate with host: no matching key exchange method found.
Their offer: diffie-hellman-group1-sha1
</pre>

В этом случае клиенту и серверу не удалось согласовать алгоритм обмена ключами, поскольку сервер предложил только один метод `diffie-hellman-group1-sha1`.

### Как это исправить

Лучшим решением для разрешения этой ситуации будет обновление/настройка сервера для того, чтобы не использовать устаревшие алгоритмы. Если же это невозможно, то можно заставить клиента снова включить алгоритм обмена ключами `diffie-hellman-group1-sha1` с помощью `-oKexAlgorithms=+diffie-hellman-group1-sha1` опции в командной строке:

```
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 user@host
```

или в файле `~/.ssh/config`:

```
Host somehost.example.org
	KexAlgorithms +diffie-hellman-group1-sha1
```