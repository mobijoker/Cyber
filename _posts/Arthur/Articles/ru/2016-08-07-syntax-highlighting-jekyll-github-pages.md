---
title: Подсветка синтаксиса кода в Jekyll
ref: syntax-highlighting-jekyll
permalink: /ru/web/syntax-highlighting-jekyll.html
author: Arthur Gareginyan
translator: Milena Kiseleva
lang: ru
layout: post
categories:
  - web
tags:
  - code highlighter
  - code-highlighter
  - code highlight
  - code-highlight
  - highlighter
  - jekyll
  - github pages
  - rouge
  - rouge theme
  - pygments theme
  - highlighter theme
  - rouge styles
  - rouge style shhet
  - таблицы стилей
  - стили
  - подсветка синтаксиса
  - подсветка кода

---

![thumb](/images/thumbnail/jekyll-rouge.png)
Jekyll имеет встроенную поддержку [подсветки синтаксиса](https://en.wikipedia.org/wiki/Syntax_highlighting) кода для более чем 100 языков. Используя подсветку в кусочках кода на твоём GitHub Pages вебсайте ты сделаешь код более читаемым. В этой статье я покажу то, как ты можешь интегрировать Rouge в твою Jekyll установку.

<br>
<br>

[Rouge](http://rouge.jneen.net/) это инструмент для посветки синтасиса кода основанный на чистом Ruby. Он может подсветить 100 различных языков, и выводить HTML или ANSI 256-цветный текст. Его выводной HTML совместим с таблицами стилей, предназначенных для Pygments. Rouge - дефолтный выделитель синтаксиса в Jekyll 3 и выше.


### Настройка

С тех пор как GitHub Pages have upgraded Jekyll до версии 3 ты можешь использовать Rouge в комбинации с Jekyll расположенном на GitHub Pages нативно. Для того чтобы подсветка синтаксиса работала в Jekyll 2, тебе нужно вручную включить Rouge подсветку синтаксиса. Чтобы это сделать, просто добавь следующую строку в `_config.yml` файл который расположен в root директории твоего Jekyll вебсайта, и убедись в том, что `rouge` gem правильно инсталлирован.

**1)** Открой фаил `_config.yml` и добавь следующую строку:

```yaml
highlighter: rouge
```

**2)** Открой терминал и впиши следующую комманду (это не требуется, если ты просто клонировал начальную точку из какого-то GitHub репозитория вместо создания нового boilerplate вебсайта используя `jekyll new`):

```sh
gem install rouge
```


### Тема (цвета)

Rouge совместим с подсветкой синтаксиса Pygments, что значит то, что мы можем использовать [таблицы стилей созданные для Pygments](https://github.com/richleland/pygments-css). Ты можешь копировать любой из этих файлов и использовать их. Предварительный просмотр этих тем доступен [здесь](http://richleland.github.io/pygments-css/). Но в моем блоге я использую тему [Son of Obsidian](https://github.com/vgaidarji/vgaidarji.github.io/blob/master/css/theme-son-of-obsidian.css).

Просто замени на новое содержимое файла с таблицей стилей для дефолтной темы подсветки синтаксиса.

Мой Jekyll вебсайт имеет `_syntax-highlighting.scss` файл расположенный в `_scss` директории. Этот файл содержит дефолтную таблицу стилей для подсветки синтаксиса. Если твой вебсайт не имеет этого файла, тот файл который отвечает за подсветку синтаксиса, или сделай следущее.

**1)** Выбери тему, которая тебе нравится по ссылке выше.

**2)** Копируй CSS фаил темы (например `monokai.css`) в `your-blog-root-directory/css/` дирректорию.

**3)** Открой `your-blog-root-directory/css/main.css` файл и добавь `monokai.css` тему:

```css
@import url(monokai.css);
```

Но это ещё не всё. Все Pygments темы используют `.codehilite` как дефолтный класс. Тоесть тебе нужно открыть для редоктирования CSS файл темы и заменить все `.codehilite` на `.highlight` класс.


### Использование

При написании Markdown с некоторым кодом для Jekyll, ты можешь включить подсветку синтаксиса так:

```
{% raw %}
{% highlight python %}
x = ('a', 1, False)
{% endhighlight %}
{% endraw %}
```

Аргумент у `highlight` тега (`python` в приведенном выше примере) это идентификатор языка. Для того, чтобы найти подходящий идентификатор для языка, который ты хочешь подсветить, смотри "short name" на [Rouge wiki](https://github.com/jayferd/rouge/wiki/List-of-supported-languages-and-lexers).

Однако это становится немного сложным, если ты постоянно переключаешся между кодом и текстом.

По умолчанию Jekyll устанавливает параметры для `fenced_code_blocks` в `true` что значит то, что ты можешь определить блок кода с помощью тройных обратных кавычек. Просто оберни свой код в тройные обратные кавычки:

	```
	Some code.
	```

Я рекомендую поместить пустую строку перед и после блока кода для того, что бы сделать чтение кода более лёгким.

Кроме того, можно передать имя языка для того, чтобы подсветить особенности языка:

	`​``javascript
	Some code.
	`​``

Обрати внимание на `javascript` после первой пары тройных обратных кавычек. Это идентификатор языка. Для того, чтобы найти подходящий идентификатор для языка, который ты хочешь подсветить, смотри "short name" на [Rouge wiki](https://github.com/jayferd/rouge/wiki/List-of-supported-languages-and-lexers).
