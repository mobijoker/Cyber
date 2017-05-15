---
title: Detect an ad blocker and show a message
ref: detect-ad-blocker-show-message
permalink: /web/detect-ad-blocker-show-message.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - how to
  - tutorial
  - jquery
  - js
  - javascript
  - ad
  - ads
  - ad blocker
  - ads blocker
  - adblock

---

![thumb](/images/articles/detect-ad-blocker-show-message/thumbnail.png)
For many websites that publish content for free, ads are one of the primary sources for getting revenue. This revenue is spent for paying the expenses to run the website. Reduction of the displayed ads means less revenue. If you're finding that the majority of your website's visitors are blocking ads then you might want to try displaying a friendly message asking them to disable the ad blocker extension that they have installed in web browser. In this article I'll show you how I detect the ad blockers and show the message to visitors of my website.


## How ad blockers work?

When we visit any website our web browser downloads an HTML file which includes an internal and external references to JavaScript files, CSS stylesheets, images and etc. If our browser has an ad blocker extension installed, it will compare the names of referenced files against a built-in block list and if there are any matches those files will be blocked. All block lists include a reference to `ads.js` because it's a common name for JavaScript files that are associated with serving ads.

Now, step by step guide.


## Step 1 - Add a message on website

First of all, we need to create a banner with friendly message asking to disable ad blocker. For this we place the following code anywhere in our theme where we would like to display the message.

```html
<div id="banner-12345">
	Our website is made possible by displaying online advertisements to our visitors.<br>
	Please consider supporting us by disabling your ad blocker on our website.
</div>
<style>
	#banner-12345 {
		display: none;
		margin-bottom: 30px;
		padding: 20px 10px;
		border-radius: 5px;
		background: #D30000;
		color: #fff;
		text-align: center;
		font-weight: bold;
	}
</style>
```

> **Note:** This message will be hidden by default.

> **Note:** You can add this code in any place of your theme: inside the post content, in the sidebar area, in the footer area and etc.. I added this code right after `<header>` tag.

> **Note:** You can style your banner the same way you would style any other part of your blog/website theme. Use a style that suits your needs.

Here’s how the message will looks like:

<div id="banner-839275452839">
	Our website is made possible by displaying online advertisements to our visitors.<br>
	Please consider supporting us by disabling your ad blocker on our website.
</div>
<style>
	#banner-839275452839 {
		margin-bottom: 30px;
		padding: 20px 10px;
		border-radius: 5px;
		background: #D30000;
		color: #fff;
		text-align: center;
		font-weight: bold;
	}
</style>


## Step 2 - Create the "ads.js" file and include to the website

Before we move on to the next step, we need to add an additional JavaScript file to our website, which is necessary to detect the ad blocker. This file, if is included to website, will create a hidden DIV element and add it to the our website's HTML source code.

For this we will create a new JavaScript file inside the root directory of our website and call it `ads.js`. Then we place the following code to this file:

```js
var e = document.createElement('div');
e.id = 'test-block';
e.style.display = 'none';
document.body.appendChild(e);
```

We will include this file (`ads.js`) by placing the following HTML code within our website's HTML source code just above the `</body>` tag:

```html
<script src="/ads.js" type="text/javascript"></script>
```

> **Note:** You can use any method of including a JS file that is best suitable for you.


## Step 3 - Check if "ads.js" was blocked

Now it's time to create code that will check the existence of our hidden DIV element. If the hidden DIV element created by our `ads.js` file exists then ads are allowed, if not then ads are blocked. And if ads are blocked we will make visible the message that we have created on the 1th step.

For this we will add the following jQuery code to the main JavaScript/jQuery file of our website:

```js
if ( $('#test-block').length == 0 ) {
    $('#banner-12345').show();
}
```

Or, if our website does not have a main JavaScript/jQuery file included, we can place the following JavaScript within our website's HTML source code just above the `</body>` tag.

```html
<script type="text/javascript">
	if ( !document.getElementById('test-block') ) {
	    document.getElementById('banner-12345').style.display='block';
	}
</script>
```


And we are done!


## Summarizing

This way I have detect the ad blokers and show a message to visitors of my website. Now when you know how it works, please disable the ad blocker on this website. Why not give these method a try before implementing on your blog/website? :)

If you were able to implement this on your blog/website then please leave a comment.

Thanks for reading!