---
lang: en
ref: how-to-fix-codemirror-editor-is-not-loading-content-until-clicked
title: 'How to fix: CodeMirror editor is not loading content until clicked'
date: 2015-09-27T21:53:32+00:00
author: Arthur Gareginyan
layout: post
permalink: /web/how-to-fix-codemirror-editor-is-not-loading-content-until-clicked.html
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
I am used CodeMirror 5 in different projects. Now I using it with WordPress plugin API and it’s working perfectly except that the editor is not loading all content until clicked. Nothing appears below line 26 until you click the mouse below that line. The content is there, but it is not visible. It just comes up as a large blank white space. If you click above it, it doesn't appear, you need to click below it.


In my WordPress plugin, there is a `textarea`, and i am replacing it with CodeMirror editor.

This is a Javascript that I use:

```js
var editor = CodeMirror.fromTextArea(document.getElementById('codeEditor'), {
	lineNumbers: true,
	matchBrackets: true,
	mode: 'application/x-httpd-php',
	indentUnit: 4
});
```


All of the CodeMirror editor work as expected so I figured maybe the `textarea` isn't focused so I tried to calling `focus()` on the DOM element.

jQuery:

```js
$("#editor").focus();
```

Javascript:

```js
document.getElementById( 'editor' ).focus();
```

But it is not worked because you need to click below the line 26 and not above.

Then I tried to call `refresh()` method after editor is made visible:

```js
setTimeout(function() {
	editor.refresh();
},1);
```

The above Javascript code will refresh the CodeMirror editor after 1 second.

And it’s work.

Now, all Javascript code looks like this:

```js
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
