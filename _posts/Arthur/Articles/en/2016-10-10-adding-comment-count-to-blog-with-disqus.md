---
title: Adding a comment count to your blog with Disqus
ref: adding-comment-count-to-blog-with-disqus
permalink: /web/adding-comment-count-to-blog-with-disqus.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - disqus
  - comment system
  - comments
  - comment count
  - guide

---

![thumb](/images/thumbnail/disqus.png)
Most blog owners that uses the Disqus comments system want to display the comment count for each page with comments, on their home page. Luckily Disqus has built in support for comment count. The setup isn't difficult, but does require a bit of theme editing.

<br>
![center](/images/adding-comment-count-to-blog-with-disqus/disqus-comment-count.png)

## **Step 1.** Add the Disqus comment count script

Find the file of your theme that is responsible for display the Home page of your blog. Depending on your website platform (WordPress, Joomla, Jekyll, and etc) this file may have the name such as `home.php`, `index.html`, `default.html`, or another name.

Then place the following code before the closing `</body>` tag in this file:

```
<script id="dsq-count-scr" src="//EXAMPLE.disqus.com/count.js" async></script>
```

> **Note:** Change the `EXAMPLE` to ShortName of your Disqus forum. Your ShortName can be found on your forum's `Admin` → `Setup` → [Identity](http://disqus.com/admin/settings/) page.


## **Step 2.** Add the comment count link

Find the place where you want to display the comment count. I chooses a section of post meta-information (section with the date and name of the author). Then place the following code to this place:

```
<a href="URL#disqus_thread">Comments</a>
```

> **Note:** Change the `URL` to URL of your post. This will tell Disqus which links to look up so it can return the correct comment count.

<br>
And you're done! Now your posts will have comments counts that will update automatically, and you can style the output the same way you would style any other part of your blog's theme.

