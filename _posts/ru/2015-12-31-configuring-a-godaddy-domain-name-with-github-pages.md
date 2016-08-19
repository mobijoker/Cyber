---
lang: ru
ref: configuring-a-godaddy-domain-name-with-github-pages
title: 'Привязка GoDaddy доменного имени к GitHub страницам'
date: 2015-12-31T14:26:30+00:00
author: Arthur Gareginyan
layout: post
permalink: /ru/web/configuring-a-godaddy-domain-name-with-github-pages.html
categories:
  - Web
tags:
  - domain
  - domain name
  - github
  - github pages
  - godaddy
  - pages

---

![thumb](/images/github-godaddy.png)
GitHub страницы это невероятно лёгкое и удобное решение для хостинга простого личного веб-сайта. По умолчанию адрес будет `username.github.io`. Ниже я объясню, как я настроил мою страницу пользователя github.io с моим собственным доменным именем `arthurgareginyan.com` которое Я зарегистрировал с помощью GoDaddy.com.


### Шаг 1. Настройка страницы пользователя github.io и регистрация доменного имени

Я предполагаю, что это уже сделано. Я создал страницу пользователя на `arthurgareginyan.github.io`. Когда Я перехожу на эту страницу, URL-адрес остаётся `arthurgareginyan.github.io` (то есть, он никуда не перенаправляет). С помощью GoDaddy.com, я зарегистрировал доменное имя `arthurgareginyan.com`. Теперь я хочу привязать моё собственное доменное имя (`arthurgareginyan.com`) к моей странице GitHub.


### Шаг 2. Создание CNAME файла в GitHub

**a)** Войдите в свой аккаунт GitHub.

**b)** Перейдите в корневой каталог вашей страницы, в моем случае это - `arthurgareginyan.github.io`.

**c)** Создайте гновфй файл с названием `CNAME` (все буквы большие, без расширения).

**d)** Поместить в файл имя домена, в моем случае это - `www.arthurgareginyan.com` (без `http://`, только апекс домен `arthurgareginyan.com` или с субдоменом, например как `www.`).

<img src="/images/godaddy-1.png" alt="github & godaddy" width="1024" height="541" />

**e)** Примените изменения.

**Note:** Можно использовать субдомен `www.` вместе с апекс-доменом. Это настраивается с помощью файла CNAME. Например:

* Если ваш CNAME файл содержит `example.com`, то `www.example.com` будет переадресовывать на `example.com`.
* Если ваш CNAME файл содержит `www.example.com`, то `example.com` будет переадресовывать на `www.example.com`.



**Note:** Аналогичным способом можно добавить файл `robots.txt` на вашу страницу GitHub. 


### Шаг 3. Настройка DNS в GoDaddy

**a)** Войдите в свой аккаунт GoDaddy.

**b)** Перейдите в раздел "Manage Your Domains".

**c)** Выберите доменное имя которое вы хотите привязать к вашей github.io странице.

**d)** Перейдите на вкладку "DNS Zone File".
<img src="/images/godaddy-2.png" alt="github & godaddy" width="1024" height="541" />

**e)** В разделе "A (Host)" добавьте две А-записи:

* Первая: "A (Host)" запись с `host` = `@` и `Points to` = `192.30.252.153`.
* Вторая: "A (Host)" запись с `host` = `@` и `Points to` = `192.30.252.1534`.


<img src="/images/godaddy-4.png" alt="github & godaddy" width="1024" height="541" />

Об этом можно прочитать здесь: https://help.github.com/articles/tips-for-configuring-an-a-record-with-your-dns-provider/

**f)** В разделе "CName (Alias)" добавьте "CNAME (Alias)" запись с `host` = `www` и `Points to` = `username.github.io` (в моём случае это - `arthurgareginyan.github.io`).

<img src="/images/godaddy-3.png" alt="github & godaddy" width="1024" height="541" />

**g)** Сохраните изменения.

Это всё, что я сделал в GoDaddy. Я не изменял ничего больше, включая записи Nameserver (NS).


### Шаг 4. Тестирование

Изменения требуют некоторого времени и не вступят в силу немедленно. Терпеливо подождите пока настройки DNS обновятся. Это может занять до 48 часов.

Когда DNS обновятся, вы должны быть в состоянии перейти на ваш собственный домен и увидеть вашу страницу `username.github.io`, но теперь с новым адресом.

Вы можете проверить вашу работу с помощью следующей команды:

```sh
dig arthurgarginyan.com +nostats +nocomments +nocmd
```

<pre>
;arthurgarginyan.com
arthurgarginyan.com.   73  IN  A 192.30.252.153
arthurgarginyan.com.   73  IN  A 192.30.252.154
</pre>

Вы можете проверить мою страницу GitHub на <a href="http://arthurgareginyan.com" target="_blank">http://arthurgareginyan.com</a>.
