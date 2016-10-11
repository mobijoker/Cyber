---
title: Добавление счётчика комментариев в блог с Disqus
ref: adding-comment-count-to-blog-with-disqus
permalink: /ru/web/adding-comment-count-to-blog-with-disqus.html
author: Arthur Gareginyan
translator: Milena Kiseleva
lang: ru
layout: post
categories:
  - web
tags:
  - disqus
  - comment system
  - comments
  - comment count
  - guide
  - комментарии
  - счётчик комментариев
  - счёт комментариев
  - система комментариев

---

![thumb](/images/thumbnail/disqus.png)
Большинство владельцев блогов, которые используют систему комментариев Disqus хотят отоброжать счётчик комментариев к каждой странице с комментариями, на их главной странице. К счастью Disqus имеет встроенную поддержку для подсчёта комментариев. Установка не сложная, но потребует некоторого редактирования темы.

<br>
![center](/images/adding-comment-count-to-blog-with-disqus/disqus-comment-count.png)

<br>
**Шаг 1.** Добавляем Disqus скрипт подсчёта комментариев.

Найди файл в твоей теме который отвечает за показ главной страницы твоего блога. В зависимости от платформы твоего веб-сайта (WordPress, Joomla, Jekyll, и т.д.) этот файл может иметь название как `home.php`, `index.html`, `default.html`, или другое.

Затем помести следующий код, перед закрывающим `</body>` тэгом в этом файле:

```
<script id="dsq-count-scr" src="//EXAMPLE.disqus.com/count.js" async></script>
```

Примечание: Замени `EXAMPLE` на ShortName твоего Disqus форума. Ты можешь найти свой ShortName на странице `Admin` → `Setup` → [Identity](http://disqus.com/admin/settings/) твоего форума.


<br>
**Шаг 2.** Добавляем ссылку подсчёта комментариев.

Найди место где ты хочешь отобразить счётчик комментариев. Я выбрал область мета-информации поста (область с датой и именем автора поста). Затем помести в это место следующий код:

```
<a href="URL#disqus_thread">Comments</a>
```

Примечание: Замени `URL` на URL твоего поста. Это скажет Disqus какие ссылки смотреть для того, что бы он мог вернуть правильный счётчик комментариев.

<br>
Готово! Теперь твои посты будут иметь счётчик комментариев, который будет обновляться автоматически, и ты сможешь стилизовать его таким же способом как и остальные части темы твоего блога.

