---
title: Relpace the Rouge highlighter with Prism.js in Jekyll
ref: relpace-rouge-highlighter-prismjs-jekyll
permalink: /web/relpace-rouge-highlighter-prismjs-jekyll.html
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

![thumb](/images/thumbnail/prismjs.png)
By default Jekyll 3, ships with [Rouge](http://rouge.jneen.net/) syntax highlighter. But for some reasons you may want to replace it with [Prism.js](http://prismjs.com) syntax highlighter. Prism.js is a very lightweight JavaScript library to provide code highlighting on websites. In this article I will show you how to set up it on Jekyll-based website.

<br><br>

**Step 1.** First, we need to disable the Rouge syntax highlighter that is Jekyll's default (bult-in in version 3) syntax highlighter. To do this, read another my post [here](http://mycyberuniverse.com/web/disable-rouge-syntax-highlighter.html).


<br>
**Step 2.** The Prism.js syntax highlighter consists of two parts, a JavaScript file and a CSS file with color scheme for it. These files can be download from [the project website](http://prismjs.com/download.html). There, a configuration tool lets you choose the languages you want included, then gives you a `prism.js` and `prism.css` files with only those languages included.


<br>
**Step 3.** Move both downloaded files to the appropriate directories that placed in the root of your Jekyll website. The `prism.js` file to `js` catalog and the `prism.css` file to `css` catalog.


<br>
**Step 4.** Include the `prism.css` in the `head.html` file, just above the ending `</head>` tag:

```html
{% raw %}<link rel="stylesheet" href="{{ "/css/prism.css" | prepend: site.baseurl }}">{% endraw %}
```


<br>
**Step 5.** Include the `prism.js` in the `footer.html` file, just above the ending `</footer>` tag:

```html
{% raw %}<script src="{{ "/js/prism.js" | prepend: site.baseurl }}"></script>{% endraw %}
```


<br>
**Step 6.** The last part is actually using the Prism.js syntax highlighter within one of your posts. Say you are writing a new post (using markdown) with code. Just wrap the code with a triple backticks:

	```
	Some code.
	```

You can also pass in a language to provide language specific highlighting:

	```javascript
	Some code.
	```

<br>

Congratulations! Now you have Prism.js syntax highlighting.
