---
title: Отключение Rouge - встроенной подсветки синтаксиса в Jekyll
ref: disable-rouge-syntax-highlighter
permalink: /ru/web/disable-rouge-syntax-highlighter.html
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

---

![thumb](/images/thumbnail/jekyll-rouge.png)
По умолчанию Jekyll версии 3, ставится с подсветкой синтаксиса от Rouge. По некоторым причинам вы можете захотеть отключить его. Например если вы заменили встроенный Rouge на другой плагин подсветки синтаксиса, как Prism.js или на ваш собственный кастомный.

<br>
<br>

Для отключения Rouge в Jekyll 3, сделайте следующее.

1. Откройте `_config.yml` файл размещённый в root директории вашего вебсайта построенного на Jekyll. 

2. Добавьте следующую строку:

```yaml
highlighter: none
```

Теперь вы отключили подсветку синтаксиса от Rouge.

<br>

Но это не работает с вебсайтами построенными на Jekyll которые хостятся на GitHub Pages. В таком случае, нам нужно сделать кое-что с `syntax_highlighter_opts`. Вместо `highlighter: none` добавьте следующие строки:

```yaml
markdown: kramdown
kramdown: 
	syntax_highlighter_opts:
		disable : true
```

Это также сработает с подсветкой синтаксиса на GitHub Pages.
