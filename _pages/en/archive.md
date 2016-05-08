---
layout: page
title: Archive
lang: en
ref: archive
order: 5
permalink: /archive.html

---
{% assign posts=site.posts | where:"lang", page.lang %}
{% for post in posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
