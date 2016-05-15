lang: en
title: Add Google Analytics to a Jekyll website
date: 2013-05-11T23:32:03+00:00
author: Arthur Gareginyan
layout: post
ref: add-googe-analytics-to-a-jekyll-website
permalink: /web/add-googe-analytics-to-a-jekyll-website.html
categories:
  - web
tags:
  - web
  - safari
  - img
  - image
  - html
  - css

---

![thumb]()

img in Safari gets hidden

---

I have three icons (links with images inside) on my website that I want to link to my GitHub, Linked In and email accounts. It works fine on Chrome but for some reason Safari adds a bunch of styles to the Linked In icon that make it hidden.

Here's the code for the three links (the links have been changed):

```
<a href="http://github" target="_blank">
    <img src="img/github.png" alt="GitHub">
</a>

<a href="http://linked in" target="_blank">
    <img src="img/linkedin.png" alt="LinkedIn">
</a>

<a href="mailto:me@mail.com">
    <img src="img/email.png" alt="E-mail">
</a>
```

This is the styling for the links (I'm using SASS so the styles are nested):

```
a {
    position:relative;
    padding-right:25px;
    padding-left:25px;

    img {
        width:64px;
        height:64px;
    }
}
```

In Chrome, this works exactly the way I want it to, when I inspect the page, this is what it shows:

```
CODE
```

But for some reason, in Safari, the Linked In icon is hidden, and the inspector shows this:

```
CODE
```

The inspector shows this for the Linked In image:

```
<img src="img/linkedin.png" alt="LinkedIn" style="display: none !important; visibility: hidden !important; opacity: 0 !important; background-position: 0px 0px;" width="0" height="0">
```

Any thoughts on why Safari is doing this, and how I could fix it would be appreciated, thanks!

---
Do you have some kind of Ad/Social Media Blocker running in Safari? 

---

```
<img src="/images/adsense-logo-2.png" alt="thumb" width="0" height="0" style="display: none !important; visibility: hidden !important; opacity: 0 !important; background-position: 0px 0px;">
```


```
<img src="/images/adsense-logo-2.png" alt="thumb">
```

---

Doh! I had AdBlock installed on Safari, and that was blocking the image. Disabled AdBlock and it works just fine.

---
GOOGLE SEARCH:
	jekyll style="display: none !important; visibility: hidden !important; opacity: 0 !important; background-position: 0px 0px;"