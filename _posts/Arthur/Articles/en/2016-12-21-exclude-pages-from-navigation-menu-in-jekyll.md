---
title: 'Exclude Pages from Navigation Menu in Jekyll'
ref: exclude-pages-from-navigation-menu-in-jekyll
permalink: /exclude-pages-from-navigation-menu-in-jekyll.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - development
  - web
tags:
  - jekyll
  - blog
  - menu
  - blog menu
  - jekyll menu
  - jekyl navigation menu
  - menu item
  - navigation menu
  - navigation menu item
  - hide menu item
  - hide navigation menu item
  - exclude page from menu
  - exclude page from navigation menu
  - exclude item from navigation menu
  - exclude item from menu

---

![thumb](/images/thumbnail/jekyll.png)
My Jekyll based website have a small number of first-tier pages that I would like to display in the navigation menu, but I also have some second-tier pages that I would like to not junk up the navigation menu. There are many ways to exclude pages from the navigation menu in Jekyll, but I'm trying to avoid using plugins, because I believe that the simplest solution is to just exclude second-tier pages from the navigation menu entirely. One quick and easy way I found is to simply harness the power of Jekyll’s Front-matter for any page I want to exclude. It’s a simple two-step process.


<br><br>

## Step 1. Front-matter section.

Create a custom variable `exclude: true` in the Front-matter section of the page that you don’t want to be automatically added:

```
---
title: Some Title
layout: default
exclude: true
---
```

## Step 2. Loop of navigation menu.

Find your main navigation menu template (by default, this is in `_includes/header.html` file). You need the loop code that locks like this (this is boilerplate Jekyll):

```
{% raw %}{% for page in site.pages %}
	<a class="page-link" href="{{ page.url | prepend: site.baseurl }}">
		{{ page.title }}
	</a>
{% endfor %}{% endraw %}
```

Now just add an unless clause around the `a` tag in order to get this:


```
{% raw %}{% for page in site.pages %}
	{% unless page.exclude %}
		<a class="page-link" href="{{ page.url | prepend: site.baseurl }}">
			{{ page.title }}
		</a>
	{% endunless %}
{% endfor %}{% endraw %}
```

In this loop we ask to check the `exclude` variable in the Front-matter section of the page, so if this variable is set to `true` then don't add this page to navigation menu.

Done! That page is now safely hidden until you link to it in manual way.
