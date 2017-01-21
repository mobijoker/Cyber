---
title: Архив
lang: ru
ref: archive
order: 5
author: Arthur Gareginyan
layout: page
permalink: /ru/archive.html

---

{% assign posts=site.posts | where:"lang", page.lang %}

{% assign counter = 0 %}
{% for item in posts %}
	{% unless item.published == false %}
		{% assign counter=counter | plus:1 %}
	{% endunless %}
{% endfor %}
Общее количество статей: {{ counter }}

{% for post in posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
{% endfor %}
