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

<section class="archive-post-list">
	{% for post in posts %}
		{% assign currentYear = post.date | date: "%Y" %}
		{% if currentYear != newYear %}
			{% unless forloop.first %}</ul>{% endunless %}
			<a name="{{ currentYear }}" class="year">
				<h1>{{ currentYear }}</h1>
			</a>
			<ul>
			{% assign newYear = currentYear %}
		{% endif %}
       <li>
       	<time>{{ post.date | date:"%d %b" }}</time>
       	&middot;
       	<a href="{{ post.url }}">{{ post.title }}</a>
       </li>
       {% if forloop.last %}</ul>{% endif %}
	{% endfor %}
</section>
