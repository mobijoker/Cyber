---
id: 680
lang: ru
ref: javascript-with-the-attribute-cf-hash-mysteriously-added-to-a-source-code
title: 'JavaScript с атрибутом “CF-Hash” таинственно добавляются к исходному коду'
date: 2015-08-11T05:06:54+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=680
permalink: /ru/web/javascript-with-the-attribute-cf-hash-mysteriously-added-to-a-source-code.html
categories:
  - Error
  - Web
tags:
  - cf-hash
  - cloudflare
  - email
  - email address obfuscation
  - error
  - javascript
  - js
  - obfuscating
  - obfuscation
  - obfuscator
  - обфускатор
  - обфускация

---

![thumb]()
Пример исходного кода:

```
scp SourceFile user@remote.host:
```

Но при посещении страницы Я вижу такой код:

```
scp SourceFile user@remote.host<script cf-hash="f9e31" type="text/javascript">
/* <![CDATA[ */!function(){try{var t="currentScript"in document?document.currentScript:function(){for(var t=document.getElementsByTagName("script"),e=t.length;e--;)if(t[e].getAttribute("cf-hash"))return t[e]}();if(t&&t.previousSibling){var e,r,n,i,c=t.previousSibling,a=c.getAttribute("data-cfemail");if(a){for(e="",r=parseInt(a.substr(0,2),16),n=2;a.length-n;n+=2)i=parseInt(a.substr(n,2),16)^r,e+=String.fromCharCode(i);e=document.createTextNode(e),c.parentNode.replaceChild(e,c)}}}catch(u){}}();/* ]]> */</script>:
```

Какой-то JavaScript добавляется к моему исходному коду (и только в одном месте).

```
<script cf-hash="f9e31" type="text/javascript">
/* <![CDATA[ */!function(){try{var t="currentScript"in document?document.currentScript:function(){for(var t=document.getElementsByTagName("script"),e=t.length;e--;)if(t[e].getAttribute("cf-hash"))return t[e]}();if(t&&t.previousSibling){var e,r,n,i,c=t.previousSibling,a=c.getAttribute("data-cfemail");if(a){for(e="",r=parseInt(a.substr(0,2),16),n=2;a.length-n;n+=2)i=parseInt(a.substr(n,2),16)^r,e+=String.fromCharCode(i);e=document.createTextNode(e),c.parentNode.replaceChild(e,c)}}}catch(u){}}();/* ]]> */</script>
```

Я стал быстро редактировать пост и увидел то, что его содержание было в порядке. Только на выходе (при показе на странице) содержание портилось. Это было очень странно. Я использую плагин для подсветки синтаксиса в примерах исходного кода, поэтому сначала Я подумал о том, что именно он вызывает ошибку. После Я решил поискать атрибут `getAttribute(“cf-hash”)` в интернете. Оказалось то, что это сервис “CloudFlare”, услугами которого Я пользуюсь, а точнее его функция обфускации почтовых адресов. 

“Email Address Obfuscation” — это функция в CloudFlare которая шифрует адреса эектронной почты на веб-странице от ботов, но сохраняя их видимыми для людей. Не происходит видимых изменений для посетителей вашего веб-сайта. CloudFlare обфусцирует адрес электронной почты по умолчанию.

Сервис “CloudFlare” ошибочно воспринимал строку `user@remote.host:` как почтовый адрес и поэтому пытался её затемнить.

Для того, чтобы исправить ситуацию необходимо экранировать строки такого вида или полностью отключить обфускацию почтовых адресов.

**1)** Чтобы запретить CloudFlare обфускацию “адреса электронной почты” (email), просто оберните их в теги комментариев HTML следующим образом:

```
<!—email_off-->EMAIL ADDRESS<!—/email_off-->
```

Любой код (например, адреса электронной почты) между открывающим и закрывающим комментарием тегов будет отображаться для пользователя точно так, как написано в исходном HTML-коде.

**2)** Для полного отключения функции обфускации почтовых адресов выполните следующие пункты. 

   1. Перейдите на сайт `www.cloudflare.com` и авторизуйтесь.

   2. Перейдите в “Dashboard”.

   3. Выберите ваш сайт.

   4. Перейдите во вкладку `Scrape Shield`.

   5. Установите в значение `off` пункт `Email Address Obfuscation`.
