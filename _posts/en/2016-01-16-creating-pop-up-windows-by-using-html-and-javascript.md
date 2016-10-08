---
lang: en
ref: creating-pop-up-windows-by-using-html-and-javascript
title: Creating pop-up windows by using HTML and JavaScript
date: 2016-01-16
author: Arthur Gareginyan
layout: post
permalink: /developing/creating-pop-up-windows-by-using-html-and-javascript.html
categories:
  - Developing
tags:
  - adobe muse
  - js pop-up
  - muse
  - pop-up
  - pop-up centered
  - pop-up javascript
  - pop-up window
  - popup
  - popup window

---

![thumb](/images/thumbnail/pop-up.png)
Pop-ups windows are some of the most common UI elements that we can find in websites. Sometimes it's useful to add a pop-up to your pages. You can use it, for example, to create a contact forms (sign-up boxes), photo galleries, or for areas of your website that you might need a link containing "more information".


In this article, you’ll see how easy it is to create a small pop-up windows, and put it on the center of screen variable to the currently selected screen resolution, by using only the HTML and JavaScript.

You can use a `TARGET="_blank"` in the `<\a>` tag, but this simply opens a new browser window that completely obscures the old one. This may be what you want, but at other times a small window on center of the large browser window is much better. This small window is popularly known as a pop-up. Using the HTML and JavaScript, you can create a pop-up window that appears when a user clicks a specific word, phrase, or graphic in a topic. This example is based on the JavaScript window `open()` method. By simply embedding a small snippet of code in your website and creating a unique link, you have complete control over the exact pixel dimensions of a link that opens in a new window.


**Step 1.** Add this javascript into the body (to the head) of your HTML document or preferably to an external javascript file:

```js
<script language="JavaScript">
  /**
   * Open centered pop-up window
   * By Arthur Gareginyan (arthurgareginyan@gmail.com)
   * For full source code, visit http://www.mycyberuniverse.com
   *
   * @param URL - specifies the URL of the page to open. If no URL is specified, a new window with about:blank will be opened
   * @param windowName - specifies the target attribute or the name of the window (_blank, _parent, _self, _top, name)
   * @param windowWidth - the window width in pixels (integer)
   * @param windowHeight - the window height in pixels (integer)
   */
   function popUpWindow(URL, windowName, windowWidth, windowHeight) {
	var centerLeft = (screen.width/2)-(windowWidth/2);
	var centerTop = (screen.height/2)-(windowHeight/2);
	var windowFeatures = 'toolbar=no, location=no, directories=no, status=no, menubar=no, titlebar=no, scrollbars=no, resizable=no, ';
	return window.open(URL, windowName, windowFeatures +' width='+ windowWidth +', height='+ windowHeight +', top='+ centerTop +', left='+ centerLeft);
   } 
</script>
```


Parameter values:

<table>
  <tr>
    <th>Feature</th>
    <th>Description</th>
  </tr>
    <th>directories=yes|no|1|0</th>
    <th>Obsolete. Whether or not to add directory buttons. Default is yes. IE only</th>
  </tr>
  <tr>
    <th>height=pixels</th>
    <th>The height of the window. Min. value is 100</th>
  </tr>
  <tr>
    <th>left=pixels</th>
    <th>The left position of the window. Negative values not allowed</th>
  </tr>
  <tr>
    <th>location=yes|no|1|0</th>
    <th>Whether or not to display the address field. Opera only</th>
  </tr>
  <tr>
    <th>menubar=yes|no|1|0</th>
    <th>Whether or not to display the menu bar</th>
  </tr>
  <tr>
    <th>resizable=yes|no|1|0</th>
    <th>Whether or not the window is resizable. IE only</th>
  </tr>
  <tr>
    <th>scrollbars=yes|no|1|0</th>
    <th>Whether or not to display scroll bars. IE, Firefox & Opera only</th>
  </tr>
  <tr>
    <th>status=yes|no|1|0</th>
    <th>Whether or not to add a status bar</th>
  </tr>
  <tr>
    <th>titlebar=yes|no|1|0</th>
    <th>Whether or not to display the title bar. Ignored unless the calling application is an HTML Application or a trusted dialog box</th>
  </tr>
  <tr>
    <th>toolbar=yes|no|1|0</th>
    <th>Whether or not to display the browser toolbar. IE and Firefox only</th>
  </tr>
</table>


**Step 2.** Add the link to any objects that you want to act as a pop-up window.

In Adobe Muse you can use hyperlink code for objects:

```js
javascript:popUpWindow('http://www.your-site.com','Example','700','600')
```

For else cases you can use one of the following hyperlinks (both are the same):

```html
<a onclick="popUpWindow('http://www.your-site.com','Example','700','600');" href="javascript:void(0);">CLICK TO OPEN POP-UP</a>
```

```html
<a href="javascript:popUpWindow('http://www.your-site.com','Example','700','600')">CLICK TO OPEN POP-UP</a>
```

**Note:** Replace the `http://www.your-site.com` with your link to page. Replace the `Example` with name of the window (`_blank`, `_parent`, `_self`, `_top`, name). Replace the '700' and '600' with needed size of the pop-up window. 

**Note:** This function doesn't work on a dual monitor setup.


### Demo

If you want to see a working example of this code then click the following:

<script language="JavaScript">
  /**
   * Open centered pop-up window
   * By Arthur Gareginyan (arthurgareginyan@gmail.com)
   * For full source code, visit http://www.mycyberuniverse.com
   *
   * @param URL - specifies the URL of the page to open. If no URL is specified, a new window with about:blank will be opened
   * @param windowName - specifies the target attribute or the name of the window (_blank, _parent, _self, _top, name)
   * @param windowWidth - the window width in pixels (integer)
   * @param windowHeight - the window height in pixels (integer)
   */
   function popUpWindow(URL, windowName, windowWidth, windowHeight) {
	var centerLeft = (screen.width/2)-(windowWidth/2);
	var centerTop = (screen.height/2)-(windowHeight/2);
	var windowFeatures = 'toolbar=no, location=no, directories=no, status=no, menubar=no, titlebar=no, scrollbars=no, resizable=no, ';
	return window.open(URL, windowName, windowFeatures +' width='+ windowWidth +', height='+ windowHeight +', top='+ centerTop +', left='+ centerLeft);
   } 
</script>

<a href="javascript:popUpWindow('http://www.mycyberuniverse.com','Example','700','600')">CLICK TO OPEN POP-UP</a>

When the user clicks on a link, a new window opens and displays a page (in this example is Home  page of this website).
