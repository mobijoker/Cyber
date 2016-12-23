---
title: 'Стили по-умолчанию для HTML5 input поля поиска в Safari и Chrome'
ref: safari-chrome-default-styles-html5-search-input
permalink: /ru/web/safari-chrome-default-styles-html5-search-input.html
author: Arthur Gareginyan
translator: Milena Kiseleva
lang: ru
layout: post
categories:
  - web
tags:
  - CSS
  - CSS properties
  - CSS styles
  - styles
  - input
  - search
  - search input
  - safari
  - chrome
  - CSS стили
  - CSS свойства
  - поле ввода
  - поле поиска
  - поисклвое поле
  - поисковая строка
  - стили
  - стилизация

---

![thumb](/images/thumbnail/search.png)
Новые input типы HTML5 форм спасают меня от тонны работы по валидации форм, а также они помогают пользователям в заполнении форм (предоставляя больше возможностей в браузере, альтернативные раскладки клавиатуры и многое другое). Это работает великолепно, но к сожалению, браузеры Safari и Chrome используют по умолчанию свои собственные таблицы стилей для этих input полей, так-что мы не можем стилизовать (добавить CSS свойства) поисковую строку самостоятельно. Мне не нужны эти встроенные в веб-браузер стили для моей поисковой строки input потому, что Я хочу использовать свои собственные CSS свойства для поисковой строки, так-что после некоторого поиска, Я нашёл решение.

<br><br>

Чтобы удалить стиль по умолчанию и разрешить твои свойства CSS для работы тебе нужно изменить `-webkit-appearance` свойство. Добавь это правило в твою таблицу стилей:

```css
input[type="search"] {
	-webkit-appearance: none;
}
```

Или, если у input поля есть имя класса, то ты можешь использовать его (для `class="search"`):

```css
.search {
    -webkit-appearance: none;
}
```

Ещё ты можешь принудить Safari и Chrome обрабатывать твою поисковую строку как типичное текстовое поле input вот так:

```css
input[type="search"] {
	-webkit-appearance: textfield;
}
```
