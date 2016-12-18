---
title: Замена выделителя Rouge на Prism.js в Jekyll
ref: relpace-rouge-highlighter-prismjs-jekyll
permalink: /ru/web/relpace-rouge-highlighter-prismjs-jekyll.html
author: Arthur Gareginyan
translator: Milena Kiseleva
lang: ru
layout: post
categories:
  - web
tags:
  - syntax highlighter
  - syntax-highlighter
  - syntax highlight
  - syntax-highlight
  - code highlighter
  - code-highlighter
  - code highlight
  - code-highlight
  - highlighter
  - jekyll
  - github pages
  - rouge
  - prism.js
  - подсветка синтаксиса
  - выделитель синтаксиса
  - синтаксис
  - подсветка кода
  - выделитель кода
  - код

---

![thumb](/images/thumbnail/prismjs.png)
По умолчанию Jekyll 3 имеет встроенный выделитель синтаксиса [Rouge](http://rouge.jneen.net/). Но по некоторым причинам ты можешь захотеть поменять его на выделитель синтаксиса [Prism.js](http://prismjs.com). Prism.js это очень лёгкая JavaScript библиотека для обеспечения выделения кода на веб-сайтах. В этой статье Я покажу тебе то, как настроить его на Jekyll веб-сайте.

<br>
<br>

**Шаг 1.** Во-первых, нам нужно отключить выдилитель синтаксиса Rouge, который является выделителем синтаксиса в Jekyll (версии 3) по-умолчанию. Чтобы сделать это, прочитай другую мою статью [здесь](http://mycyberuniverse.com/ru/web/disable-rouge-syntax-highlighter.html).


<br>
**Шаг 2.** Prism.js состоит из двух частей, JavaScript файл и CSS файл с цветовой схемой для него. Эти файлы можно скачать с [сайта проекта](http://prismjs.com/download.html). Там, инструмент конфигурации позволяет выбрать языки, которые ты хочешь включить, затем ты получишь `prism.js` и `prism.css` файлы с поддержкой только нужных тебе языков.


<br>
**Шаг 3.** Перемести оба загруженных файла в соответствующие каталоги, которые расположены в root твоего веб-сайта Jekyll. `prism.js` файл в `js` каталог и `prism.css` файл в `css` каталог.


<br>
**Шаг 4.** Включи `prism.css` в файл `head.html`, чуть выше тега `</head>`:

```html
{% raw %}<link rel="stylesheet" href="{{ "/css/prism.css" | prepend: site.baseurl }}">{% endraw %}
```


<br>
**Шаг 5.** Включи `prism.js` в файл `footer.html`, чуть выше тега `</footer>`:

```html
{% raw %}<script src="{{ "/js/prism.js" | prepend: site.baseurl }}"></script>{% endraw %}
```


<br>
**Шаг 6.** Последняя часть это использование выделителя синтаксиса Prism.js в одном из твоих постов. Допустим, ты пишешь новый пост (используя markdown) с кодом. Просто оберни код в обратные тройные кавычки:

	```
	Some code.
	```

Дополненительно ты можешь указать язык для того, чтобы обеспечить выделение особенностей определённого языка:

	```javascript
	Some code.
	```

<br>

Поздравляю! Теперь у тебя установлен выделитель синтаксиса Prism.js.
