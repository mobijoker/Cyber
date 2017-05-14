---
title: Making smart sticky elements by using a jQuery plugin
ref: making-smart-sticky-elements-using-jquery-plugin
permalink: /web/making-smart-sticky-elements-using-jquery-plugin.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - how to
  - tutorial
  - jquery
  - jquery plugin
  - js
  - javascript
  - sticky-kit
  - sticky-kit.js
  - sticky-kit.min.js
  - ad
  - ads
  - ad unit
  - sticky
  - sticky ad
  - sticky element

---

![thumb](/images/articles/making-smart-sticky-elements-using-jquery-plugin/thumbnail.png)
Sometimes when I surfing the Internet I see the sticky ellements that applied on website. Most often it's a sticky ads that placed in sidebar. Sticky ad is an ad unit that stays in place while the page scrolls. Some are fixed completely when others (often placed at the end of sidebar content) scroll until they are in view then stay in a fixed position as the user scrolls further down the page.

They are good at catching the user’s eye. Sticky ad units contribute uplift in performance metrics such as CTR and CPM without hurting quality. Actually we can use them not only for ad units, but also for sign-up boxes, message display, etc. In this article, you’ll see how easy it is to make a smart sticky elements by using the Sticky-Kit jQuery plugin.

[Sticky-Kit](http://leafo.net/sticky-kit/) is a lightweight jQuery plugin that provides an easy way to attach elements to the page when the user scrolls such that the element is always visible. The Sticky-Kit consists of only one jQuery file and because of this, it can be easy embedded in any project where JavaScript can be applied. As the author says, the Sticky Kit works with all modern browsers, and IE7+. The source can be found on [GitHub](https://github.com/leafo/sticky-kit).

> If you are using an ad network please confirm with them before using sticky ads with their ads. Some ad networks (AdSense is one of them) see using this technique as a violation to their terms of service and might ban you in case they become aware of it.



### Step 1. Include the jQuery library

Before we can begin working with jQuery, we must add the jQuery library to our project. If you haven't done that already, then you can read [this](http://mycyberuniverse.com/web/including-jquery-library-to-website.html) article to find out how to do it.


### Step 2. Include the Sticky-Kit script 

We will include the latest version (for April 2017 it’s a v1.1.2) of the Sticky-Kit to our website. For this we download the compressed version of the `sticky-kit.js` script from the [official Sticky-Kit page](http://leafo.net/sticky-kit/) and copy it into our existing project directory.

> The compressed version of the `sticky-kit.js` script is named `sticky-kit.min.js`.

Now we need to find the file of our theme that is responsible for the HEAD section of our website. Depending on your website platform (WordPress, Joomla, Jekyll, and etc) this file may have the name such as `head.php`, `index.html`, `default.html`, or another name. Then we place the following code before the closing `</head>` tag in this file:

```html
<script src="/sticky-kit.min.js"></script>
```

> In the code line above we do not have the `type="text/javascript"` inside the `<script>` tag because this is not required in HTML5. JavaScript is the default scripting language in HTML5 and in all modern browsers.

> The `/sticky-kit.min.js` in the code line above is a path to the `sticky-kit.min.js` file which we copied into our project. You may need to fix this path depending on the location of your `sticky-kit.min.js` file.

This will ensure that the `sticky-kit.min.js` script will be included to every page of our website.


### Step 3. Apply the Sticky-Kit to DOM element

Now we can apply the Sticky-Kit to any DOM element that we want to act as a sticky element. For this we will add the following jQuery code to the main JavaScript/jQuery file of our project:

```js
$("#sidebar").stick_in_parent();
```

In this example, we made that the whole sidebar act as a sticky element. We can do the same with any other element simply by replacing the `#sidebar` with the appropriate class name or ID of the DOM element.

> You can find more examples of use on the [official Sticky-Kit page](http://leafo.net/sticky-kit/) and the [Sticky-Kit Wiki](https://github.com/leafo/sticky-kit/wiki/Troubleshooting).


Done! Now your know how to make a smart sticky elements by using the Sticky-Kit jQuery plugin.

Thanks for reading!
