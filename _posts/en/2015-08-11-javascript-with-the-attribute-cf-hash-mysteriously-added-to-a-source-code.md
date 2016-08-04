---
lang: en
ref: javascript-with-the-attribute-cf-hash-mysteriously-added-to-a-source-code
title: JavaScript with the attribute “CF-Hash” mysteriously added to a source code
date: 2015-08-11T05:06:54+00:00
author: Arthur Gareginyan
layout: post
permalink: /web/javascript-with-the-attribute-cf-hash-mysteriously-added-to-a-source-code.html
categories:
  - Error
  - Web
tags:
  - cf-hash
  - cloudflare
  - email
  - email address obfuscation
  - error
  - javascript
  - js
  - obfuscating
  - obfuscation
  - obfuscator
  - обфускатор
  - обфускация

---

![thumb]()
The source code was something like this:

```sh
scp SourceFile user@remote.host:
```

But when I visited the page, it was all munged like this:

```sh
scp SourceFile user@remote.host<script cf-hash="f9e31" type="text/javascript">
/* <![CDATA[ */!function(){try{var t="currentScript"in document?document.currentScript:function(){for(var t=document.getElementsByTagName("script"),e=t.length;e--;)if(t[e].getAttribute("cf-hash"))return t[e]}();if(t&&t.previousSibling){var e,r,n,i,c=t.previousSibling,a=c.getAttribute("data-cfemail");if(a){for(e="",r=parseInt(a.substr(0,2),16),n=2;a.length-n;n+=2)i=parseInt(a.substr(n,2),16)^r,e+=String.fromCharCode(i);e=document.createTextNode(e),c.parentNode.replaceChild(e,c)}}}catch(u){}}();/* ]]> */</script>:
```

Some JavaScript is being added to my source code (and only in one place).

```js
<script cf-hash="f9e31" type="text/javascript">
/* <![CDATA[ */!function(){try{var t="currentScript"in document?document.currentScript:function(){for(var t=document.getElementsByTagName("script"),e=t.length;e--;)if(t[e].getAttribute("cf-hash"))return t[e]}();if(t&&t.previousSibling){var e,r,n,i,c=t.previousSibling,a=c.getAttribute("data-cfemail");if(a){for(e="",r=parseInt(a.substr(0,2),16),n=2;a.length-n;n+=2)i=parseInt(a.substr(n,2),16)^r,e+=String.fromCharCode(i);e=document.createTextNode(e),c.parentNode.replaceChild(e,c)}}}catch(u){}}();/* ]]> */</script>
```

I quickly edited the post and saw the content there was just fine. The only content that was getting munged was code output (in preview). It was very confusing. I use a plugin for syntax highlighting of source code examples, so at first I thought that this plugin causes an error. After I googled the attribute `getAttribute(“cf-hash”)`. I learned that this is a function of email address obfuscation from “CloudFlare” service (which I use). 

“Email Address Obfuscation” — a feature in CloudFlare that encrypt email addresses on your web page from bots, while keeping them visible to humans. There are no visible changes to your website for visitors. CloudFlare obfuscates your email address by default.

Service "CloudFlare" wrongly perceived the string `user@remote.host:` as email address and therefore tried to obscure it.

In order to fix the situation, this kind of string must be escaped or the obfuscation of email addresses must be completely disabled.

**1)** To prevent CloudFlare from obfuscating “emails”, just wrap them in HTML comment tags like this:

```html
<!—email_off-->EMAIL ADDRESS<!—/email_off-->
```

Any code (like email addresses) between the opening and closing comment tags will be displayed to the user exactly as written in the original HTML code.

**2)** To fully disable the obfuscating email addresses do the following.

   1. Go to `www.cloudflare.com` and log in.

   2. Go to the “Dashboard”.

   3. Choose your website.

   4. Go to the “Scrape Shield” tab.

   5. Set “Email Address Obfuscation” to “off”.
