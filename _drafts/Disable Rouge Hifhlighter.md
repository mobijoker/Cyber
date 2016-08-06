---
title: Disable the Rouge Syntax Highlighter in Jekyll+GithHub Pages
ref: the-title-of-post
permalink: /web/the-title-of-post.html
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
  - highlighter
  - jekyll
  - github pages
  - rouge

---

![thumb]()

It's fairly simple to set up - but there's a trick to getting it to work from a CDN. When you download `prism.js` from the project website, a configuration tool lets you choose the languages you want included, then gives you a `prism.js` with only those languages included.

By default Jekyll, ships with kramdown to convert markdown to HTML. For some reason, the output kramdown was producing wasn't the way Prism expects code blocks.

---

To get `prism.js` working in Jekyll that hosted on GitHub Pages, we need to disable the Rouge syntax highlighter that is Jekyll's default syntax highlighter. To do this, just add the following to `_config.yml` file that placed in the root of your Jekyll website.

```yaml
markdown: kramdown
kramdown: 
	syntax_highlighter_opts:
		disable : true
```

Congratulations! Now you have Prism.js syntax highlighting.