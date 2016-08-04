---
lang: ru
ref: how-to-fix-codemirror-editor-is-not-loading-content-until-clicked
title: 'How to fix: CodeMirror редактор не загружает контент до клика'
date: 2015-09-27T21:53:32+00:00
author: Arthur Gareginyan
layout: post
permalink: /ru/web/how-to-fix-codemirror-editor-is-not-loading-content-until-clicked.html
categories:
  - Error
  - Web
tags:
  - .refresh
  - codemirror
  - editor
  - error
  - issue
  - javascript
  - problem
  - textarea

---

![thumb](/images/CodeMirror.png)
Я использовал CodeMirror 5 в разных проектах. Сейчас Я использую его совместно с WordPress Plugin API и он работает отлично за исключением того, что, до клика, редактор загружает контент не полностью. Не появляется ничего ниже 26 строки до тех пор пока не будет клика мышью ниже этой строки. Контент есть, но он невидим. Это выглядит как большое пустое пространство. Если будет клик выше этой строки, ничего не появится так, как необходимо кликнуть ниже этой строки.


В моём WordPress плагине, имеется `textarea`, которое Я заменяю редактором CodeMirror.

Вот Javascript код который Я использую:

```
var editor = CodeMirror.fromTextArea(document.getElementById('codeEditor'), {
	lineNumbers: true,
	matchBrackets: true,
	mode: 'application/x-httpd-php',
	indentUnit: 4
});
```


Всё остальное в CodeMirror редакторе работает как нужно и Я подумал о том, что `textarea` просто не сфокусирован, поэтому Я попробовал вызвать `focus()` на элементе DOM.

jQuery:

```
$("#editor").focus();
```

Javascript:

```
document.getElementById( 'editor' ).focus();
```

Но это не сработало потому, что необходимо кликнуть именно ниже 26-ой строки, а не выше.

Затем Я попробовал вызвать `refresh()` метод после того как редактор станет видимым:

```
setTimeout(function() {
	editor.refresh();
},1);
```

Вышеприведённый Javascript код перезагрузит CodeMirror редактор после ожидания в 1 секунду.

И это сработало.

Теперь, весь Javascript код выглядит так:

```
var editor = CodeMirror.fromTextArea(document.getElementById('editor'), {
	lineNumbers: true,
	matchBrackets: true,
	mode: 'application/x-httpd-php',
	indentUnit: 4
});
setTimeout(function() {
	editor.refresh();
},1);
```
