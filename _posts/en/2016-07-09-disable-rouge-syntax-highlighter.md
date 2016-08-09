---
title: Disable the Rouge - Jekyll's default syntax highlighter
ref: disable-rouge-syntax-highlighter
permalink: /web/disable-rouge-syntax-highlighter.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - syntax highlighter
  - syntax-highlighter
  - syntax highlight
  - syntax-highlight
  - code highlighter
  - code-highlighter
  - code highlight
  - code-highlight
  - highlighter
  - jekyll
  - github pages
  - rouge

---

![thumb](/images/jekyll-rouge.png)
By default Jekyll version 3, ships with Rouge syntax highlighter. For some reason, you may want to disable it. For example, if you replace the built-in Rouge to another syntax highlighter such as Prism.js or your own custom highlighter.

<br>
<br>

To get Rouge disabled in Jekyll 3, just do the following. 

1. Open the `_config.yml` file located at the root directory of your Jekyll-based website.

2. Add the following line:

```yaml
highlighter: none
```

Now you have Rouge syntax highlighter disabled.

But this is not working with Jekyll-based websites that hosted on GitHub Pages. In this case, we need some trick with `syntax_highlighter_opts`. Instead of `highlighter: none` add the following lines:

```yaml
markdown: kramdown
kramdown: 
	syntax_highlighter_opts:
		disable : true
```

This will disable the syntax highlighting on GitHub Pages too.
