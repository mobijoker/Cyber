---
title: "Как исправить: Не работает всплывающее окно с подпиской MailChimp в WordPress"
ref: mailchimp-subscriber-popup-not-working-in-wordpress
permalink: /ru/mailchimp-subscriber-popup-not-working-in-wordpress.html
author: Arthur Gareginyan
translator: Milena Kiseleva
lang: ru
layout: post
categories:
  - error
  - web
tags:
  - wordpress
  - wordpress mailchimp
  - wordpress and mailchimp
  - mailchimp
  - mailchimp subscription
  - subscription popup
  - subscription
  - subscription form
  - subscribe
  - подписка
  - subscriber form
  - ошибка
  - subscriber popup
  - mailchimp popup
  - mailchimp subscriber popup
  - mailchimp всплывающее окно с подпиской
  - всплывающее окно с подпиской mailchimp
  - всплывающее окно с подпиской
  - всплывающее окно подписки
  - окно с подпиской
  - подписка mailchimp
  - окно подписки
  - всплывающая подписка

---

![thumb](/images/articles/mailchimp-subscriber-popup-not-working-in-wordpress/mailchimp.png)
MailChimp это отличное решение для того, чтобы добавить форму подписки на твой веб-сайт. Единственная проблема заключается в том, что MailChimp всплывающее окно с подпиской не работает на сайтах WordPress. Я добавил код всплывающего окна с подпиской MailChimp  на один из моих сайтов WordPress, но когда я загружал любую страницу сайта, где должено было появляться всплывающее окно, ничего не произходило. Я искал в Google и заметил то, что у многих других возникает та же проблема в WordPress.

Пример встраиваемого кода всплывающего окна с подпиской MailChimp:

```
<script type="text/javascript" src="//s3.amazonaws.com/downloads.mailchimp.com/js/signup-forms/popup/embed.js" data-dojo-config="usePlainJson: true, isDebug: false"></script>
<script type="text/javascript">require(["mojo/signup-forms/Loader"], function(L) { L.start({"baseUrl":"mc.us14.list-manage.com","uuid":"xxxxxxxxxxxxxxxxxxxxxxxxxx","lid":"xxxxxxxxxxx"}) })</script>
```


### Причины проблемы

Анализируя код страницы Я заметил то, что код для вставки всплывающего окна с подпиской MailChimp (файл `//s3.amazonaws.com/downloads.mailchimp.com/js/signup-forms/popup/embed.js`) пытается загрузить `jquery.js` файл из root дирректории веб-сайта. Но в WordPress [jquery.js](https://jquery.com/) файл расположен в `/wp-includes/js/jquery/` дирректории.


### Как это исправить

Для того, чтобы заставить его работать, тебе нужно добавить `jquery.js` файл в root дирректорию веб-сайта. Нужно создать файл с именем `jquery.js`, но содержание будет загружаться из файла `jquery.js` который входит в комплект с WordPress. Теперь пошаговая инструкция.


**Шаг 1.** [Создай твоё всплывающее окно с подпиской MailChimp](http://kb.mailchimp.com/lists/signup-forms/add-a-pop-up-signup-form-to-your-website) и скопируй код для вставки всплывающего окна с подпиской MailChimp, который будет тебе предложен.

![](/images/articles/mailchimp-subscriber-popup-not-working-in-wordpress/1.png)

**Шаг 2.** В WordPress панели администратора установи и активируй плагин [Head and Footer Scripts Inserter](https://wordpress.org/plugins/header-and-footer-scripts-inserter/).

![](/images/articles/mailchimp-subscriber-popup-not-working-in-wordpress/2.png)

**Шаг 3.** В WordPress панели администратора перейди на страницу настроек плагина (`Settings -> Head and Footer Scripts Inserter`). Вставь код (тот который ты получил в шаге 2) и нажми на кнопку `Save Changes`.
 
![](/images/articles/mailchimp-subscriber-popup-not-working-in-wordpress/3.png)

**Шаг 4.** Создай пустой текстовый файл с именем `jquery.js`. Открой его в текстовом редакторе и вставь в него следующий код:

```
jQuery.getScript("/wp-includes/js/jquery/jquery.js").done(function(){ })
```

**Шаг 5.** Используя FTP или твою cPanel File Manager перенеси файл `jquery.js` (тот который ты создал в шаге 4) в root дирректорию твоего веб-сайта. Обычно root дирректория это дирректория с именем `www` если ты используешь cPanel, или `httpdocs` если ты используешь Parallels Plesk Panel.


Готово! Теперь, когда ты загрузишь любую страницу на твоём веб-сайте, твой всплывающее окно с подпиской MailChimp должно работать.

> **Примечание:** MailChimp хранит cookie в течение одного года для того, чтобы ты не видел всплывающие окно повторно после того, как ты закрыл или заполнил его. Не попадись в ловушку, думая, что всплывающее окно не работает, когда оно на самом деле работает. Если ты тестируешь это, то тебе возможно нужно будет почистить cookies, использовать другой браузер, или открыть приватное окно браузера для того, чтобы увидеть форму при повторных посещениях после отключения или заполнения его.
