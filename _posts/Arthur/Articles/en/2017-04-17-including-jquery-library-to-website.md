---
title: Including the jQuery library to your website
ref: including-jquery-library-to-website
permalink: /web/including-jquery-library-to-website.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - how to
  - tutorial
  - jquery
  - jquery library
  - js
  - javascript
  - javascript library
  - library
  - google cdn
  - cdn
  - content delivery network

---

![thumb](/images/thumbnail/jquery.png)
In addition to custom JavaScript files many developers find jQuery useful. jQuery is the most popular JavaScript library available that allows developers to easily and quickly add enhancements to the appearance and behaviors of their projects. So developers can perform common JavaScript functions while using less code.

jQuery contains all the common DOM, event, effects, and Ajax functions. jQuery's syntax is concise and makes use of variables in the form of CSS selectors as a way of connecting an effect with any targeted element of the DOM, be it a unique element (id), or set of elements (class), or arbitrarily chosen.

Actually the jQuery library is a lightweight single JavaScript file and because of this, it can be embedded in any project where JavaScript can be applied.

If we would like to create custom JavaScript functionality using the jQuery library, we will need to include the jQuery library in our project. But if we don't want to download and host jQuery yourself, we can load it from the Google CDN (Content Delivery Network). One big advantage of using the hosted jQuery from Google: Many users already have downloaded jQuery from Google CDN when visiting another website. As a result, it will be loaded from cache when they visit your website, which leads to faster loading time. Also, Google CDN will make sure that once a user requests a file from it, it will be served from the server closest to them, which also leads to faster loading time.

We will include the latest (for April 2017 it's a v3.2.1) jQuery library to our website. For this we need to find the file of our project that is responsible for the HEAD section of our website. Depending on your website platform (WordPress, Joomla, Jekyll, and etc) this file may have the name such as `head.php`, `index.html`, `default.html`, or another name. Then we place the following code before the closing `</head>` tag in this file:

```html
<script src="//ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
```

This will ensure that the jQuery library will be loaded from the Google CDN (Content Delivery Network) and included to every page of our website.

> In the code line above we do not have the `type="text/javascript"` inside the `<script>` tag because this is not required in HTML5. JavaScript is the default scripting language in HTML5 and in all modern browsers.

> Place your jQuery `<script>` tag before any other `<script>` and `<style>` tags inside the `<head>` tag.


And here is an example of a web template with the jQuery `<script>` tag included:

```
<!doctype html>
<html>
		<head>
			<title>Your Project</title>
			<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
			<script src="//ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
			<link rel="stylesheet" type="text/css" href="style.css">
		</head>
	<body>
		...
	</body>
</html>
```

Done! Now we can begin adding jQuery functionality to our website.

Thanks for reading!
