---
title: Jekyll post not showing up
ref: jekyll-post-not-showing-up
permalink: /web/jekyll-post-not-showing-up.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - jekyll
  - github
  - post
  - not generated
  - not showing up

---

![thumb](/images/Jekyll-logo.png)
Some time ago I was faced with such a problem. I have tried to add a new post to my Jekyll website, but I could not see it on the generated pages when I run jekyll serve. So what are the some common reasons for a Jekyll post to not be generated?

<br>

* The post is not placed in the `_posts` directory.

* The post has incorrect name of file. Posts should be named `YEAR-MONTH-DAY-title.MARKUP`. For example `2016-05-30-jekyll-post-not-showing-up.md`.

* The post's date is in the future and the `future: true` directive is enabled. Jekyll recognises future posts and will not display them until that time is reached.

* Time zones. Same probleme as with future date, but you set the current time. Maybe time zone is set to UTC. Try to set the time zone of your region.

* The post has `published: false` directive in its front matter. Set it to `true`.

* Incorrect characters in the title. Most likely its contains a double colon (`:`) character. Just replace it with `&#58`.

* Can be browser cache as well if you are looking not in the `_site` folder but directly on the blog's main page with the list of posts.

<br>

By the way, there are a million other reasons why your post might not show up.