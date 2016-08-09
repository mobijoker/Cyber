---
title: Relpace the Rouge Syntax Highlighter with Prism.js in Jekyll+GithHub Pages
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
  - code highlighter
  - code-highlighter
  - code highlight
  - code-highlight
  - highlighter
  - jekyll
  - github pages
  - rouge
  - prism.js

---

![thumb](/images/prismjs.png)

Prism.js is a great JavaScript library to provide code highlighting on your websites.

a JavaScript based syntax highlighter

It's fairly simple to set up - but there's a trick to getting it to work from a CDN. When you download `prism.js` from the project website, a configuration tool lets you choose the languages you want included, then gives you a `prism.js` with only those languages included.

By default Jekyll, ships with Rouge syntax highlighter.

---

Importing support for the language you need
[The version on cdnjs](https://cdnjs.com/libraries/prism) doesn't have a configuration tool - but rather than making a big file with all languages included, the base version includes a small set of languages, and other languages can be imported by including additional components.

The base version includes support for javascript, css, 'markup' (which works on HTML, XML, and XML-based things like SVG) and 'c-like'.

Languages that you haven't imported support for will be left unstyled - as if prism.js wasn't working at all. You have to explicitly import the language support files you need. As an example, here's how to style a bash script with prism.js from cdnjs:

```
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/prism/1.5.1/themes/prism.min.css">

page content goes here

<code class="language-bash">
#!/bin/bash
set -e # Exit on failure
# bash script here!
</code>

<script src="//cdnjs.cloudflare.com/ajax/libs/prism/1.5.1/prism.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/prism/1.5.1/components/prism-bash.min.js"></script>
```

---

To get `prism.js` working in Jekyll that hosted on GitHub Pages, we need to disable the Rouge syntax highlighter that is Jekyll's default syntax highlighter. To do this, just add the following to `_config.yml` file that placed in the root of your Jekyll website.

```yaml
markdown: kramdown
kramdown: 
	syntax_highlighter_opts:
		disable : true
```

Include the required stylesheet in the `head.html` file:

In `head.html` add CSS:

```html
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/prism/1.5.1/themes/prism.min.css">
```

Include the required JavaScript in the `footer.html` file:

In `footer.html` add JS:

```html
<script src="//cdnjs.cloudflare.com/ajax/libs/prism/1.5.1/prism.js"></script>
```

Notice how we've placed our script at the bottom of the page, just before the closing body tag. This is always a smart move, as it improves performance.

And then, when writing markdown with code, just wrap the code with a triple backticks:

	```
	Some code.
	```

You can also pass in a language to provide language specific highlighting:

	```javascript
	Some code.
	```

Congratulations! Now you have Prism.js syntax highlighting.