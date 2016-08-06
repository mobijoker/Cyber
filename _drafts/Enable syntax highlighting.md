---
title: Syntax Highlighting with Rouge in Jekyll+GithHub Pages
ref: add-googe-analytics-to-a-jekyll-website
permalink: /web/add-googe-analytics-to-a-jekyll-website.html
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

You can have code snippets highlighted so that they are easier to read on your GitHub Pages website using Rouge, Jekyll's default syntax highlighter.

Rouge is Jekyll's default syntax highlighter.

Rouge is a pure-ruby syntax highlighter. It can highlight 100 different languages, and output HTML or ANSI 256-color text. Its HTML output is compatible with stylesheets designed for pygments.

It's fairly simple to set up.

In this post I will show you how you can integrate Rouge into your Jekyll setup.


### Set up

Ever since GitHub pages have upgraded Jekyll to version 3 you can use Rouge in combination with Jekyll on GitHub pages natively. To get syntax highlighting working in Jekyll that hosted on GitHub Pages, we need to enable the Rouge syntax highlighter. To do this, just add the following two lines to `_config.yml` file that placed in the root of your Jekyll website.

```yaml
markdown: kramdown
highlighter: rouge
```


### Using

When writing markdown with some code to be read by Jekyll, you can enable syntax highlighting with:

	{% highlight python %}
	x = ('a', 1, False)
	{% endhighlight %}

However, this becomes a bit verbose if you constantly switch between code and text.

By default, Jekyll sets the options for `fenced_code_blocks` to `true` which means you can define a code block with triple backticks. So just wrap your code with a triple backticks:

	```
	Some code.
	```

**Note:** I recommend placing a blank line before and after code blocks.

You can also pass a language name to provide language specific highlighting:

	`​``javascript
	Some code.
	`​``

Note the `html` after the first pair of triple backticks. This tells Rouge what language to use for the code block. You can view all supported languages with samples on [Rouge’s demo site](http://rouge.jayferd.us/demo).


### CSS Theme

Rouge is compatible with the Pygments syntax highlighter, which means that we can use [stylesheets created for Pygments](https://github.com/richleland/pygments-css). You can copy any of those files and use them. Preview of this themes available [there](http://richleland.github.io/pygments-css/).

**Note:** All of those themes uses `.codehilite` as the default class. So we need to open for edit the CSS file of theme and replace all `.codehilite` with `.highlight` class.

Just replace with new the content of `syntax.css` file that contain a style sheet of default theme of syntax highlighter. This file placed in the `css` catalog of your Jekyll website.
