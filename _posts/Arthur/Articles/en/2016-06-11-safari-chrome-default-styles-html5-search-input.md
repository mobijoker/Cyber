---
title: Safari’s and Chrome's default styles for HTML5 search input
ref: safari-chrome-default-styles-html5-search-input
permalink: /web/safari-chrome-default-styles-html5-search-input.html
author: Arthur Gareginyan
lang: en
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

---

![thumb](/images/thumbnail/search.png)
The new HTML5 form input types save me tons of work on form validation, and they’ll assist your users in filling them (by providing more in-browser features, alternate keyboard layouts and more). It works great, but unfortunately, the Safari and Chrome browsers uses their own default stylsheet for this inputs, and so you can't style (add a CSS properties) the search input yourself. I didn’t need this in-browser style for my search input, because I want to add my own CSS properties to searc input, so after some searching, I discovered the below solution.

<br><br>

To remove the default styling and allow your CSS properties to work you need to change the `-webkit-appearance` property. Add this rule to your stylesheet:

```css
input[type="search"] {
	-webkit-appearance: none;
}
```

Or, if the input have a class name, you can use it (for `class="search"`):

```css
.search {
    -webkit-appearance: none;
}
```

Also you can force Safari and Chrome to treat your search input like a typical text field input by this:

```css
input[type="search"] {
	-webkit-appearance: textfield;
}
```
