---
lang: en
ref: disabling-right-clicking-by-using-javascript
title: Disabling right-clicking by using JavaScript
date: 2016-01-23
author: Arthur Gareginyan
layout: post
permalink: /developing/disabling-right-clicking-by-using-javascript.html
categories:
  - Developing
tags:
  - disable click
  - disable right click
  - mouse click
  - mouse right click
  - prevent click
  - prevent right click
  - restrict click
  - restrict right click
  - right click javascript
  - right click js
  - right mouse
  - right-click
  - right-clicking
  - turning off right click

---

![thumb](/images/thumbnail/mouse-right-click.png)
It makes sense to do everything you can to protect your copyrighted content. While there is no way to completely stop people from stealing your images, you can make it harder. Disabling right-clicking is one method you can use to deter casual theft.


On one of my websites, I have a pop-up page where I placed gallery with my copyrighted images. I don't want the user to see the menu thats get displayed with the mouse right click. So I created the HTML/JavaScript code that will prevent the default right menu from popping up when the right mouse is clicked on this pop-up page. Now I use it to stop surfers from easily stealing my copyrighted images from my website.

Simply add the following code to the <BODY> section of your web page (Press Ctrl C after selecting code to copy it) :

```js
<script language="JavaScript">
/**
  * Disable mouse right-click on page
  * By Arthur Gareginyan (arthurgareginyan@gmail.com)
  * For full source code, visit http://www.mycyberuniverse.com
  */
document.addEventListener("contextmenu", function(e){
    e.preventDefault();
}, false);
</script>
```

The HTML code above have a simple inline JavaScript code:

```js
document.addEventListener("contextmenu", function(e){ e.preventDefault(); }, false);
```


### Demo

Mouse right click is disabled in this page. You can test it by right clicking anywhere in this page.


### Browser support

Maybe, this is not a cross browser JavaScript code. I tested it only in Safari 9 and Firefox 42.


### Don't do it

However I have to say that this should not be done generally because it limits users options and it isn't really going to protect your content (if that is what you are trying achieve). You will have to use JavaScript to accomplish this. If the user has JavaScript disabled, you cannot prevent the right click.

The right menu is there for a reason, and it should be left there. Many browser extensions add entries to the right click menu and the user should be able to use it in any page he visits.

The following article better explains why this should not be done and what other actions can be taken to solve common related issues: <a href="http://www.sitepoint.com/dont-disable-right-click/" target="_blank">http://www.sitepoint.com/dont-disable-right-click/</a>

**P.S.**
If really you cannot resist the urge to block it at least do not put a popup saying "no right click allowed".

<script language="JavaScript">
/**
  * Disable mouse right-click on page
  * By Arthur Gareginyan (arthurgareginyan@gmail.com)
  * For full source code, visit http://www.mycyberuniverse.com
  */
document.addEventListener("contextmenu", function(e){
    e.preventDefault();
}, false);
</script>
