---
title: Syntax Highlighting in Jekyll
ref: syntax-highlighting-jekyll
permalink: /web/syntax-highlighting-jekyll.html
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
  - rouge theme
  - pygments theme
  - highlighter theme
  - rouge styles
  - rouge style shhet

---

![thumb](/images/thumbnail/jekyll-rouge.png)
Jekyll has built in support for [Syntax Highlighting](https://en.wikipedia.org/wiki/Syntax_highlighting) of over 100 languages. You can have code snippets highlighted so that they are easier to read on your GitHub Pages website. In this post I will show you how you can integrate Rouge into your Jekyll setup.

<br>
<br>

[Rouge](http://rouge.jneen.net/) is a pure-ruby syntax highlighter. It can highlight 100 different languages, and output HTML or ANSI 256-color text. Its HTML output is compatible with stylesheets designed for Pygments. Rouge is the default highlighter in Jekyll 3 and above.


### Set up

Ever since GitHub pages have upgraded Jekyll to version 3 you can use Rouge in combination with Jekyll that hosted on GitHub Pages natively. To get syntax highlighting working in Jekyll 2, we need to enable the Rouge syntax highlighter. To do this, just add the following one line to `_config.yml` file that placed in the root of your Jekyll website, and ensure the `rouge` gem is installed properly.

1. Open the `_config.yml` file and add the following line:

```yaml
highlighter: rouge
```

2. Open the terminal and enter the following command (this not needed if you just clone a starting point from some GitHub repository instead of create a new boilerplate website using `jekyll new`):

```sh
gem install rouge
```


### Theme (colors)

Rouge is compatible with the Pygments syntax highlighter, which means that we can use [stylesheets created for Pygments](https://github.com/richleland/pygments-css). You can copy any of those files and use them. Preview of this themes available [there](http://richleland.github.io/pygments-css/). But on my blog I use the [Son of Obsidian](https://github.com/vgaidarji/vgaidarji.github.io/blob/master/css/theme-son-of-obsidian.css) theme.

Just replace with new the content of file that contain a style sheet of default theme of syntax highlighter.

My Jekyll website have the `_syntax-highlighting.scss` file located in `_scss` directory. This file contains the default style sheet for syntax highlighter. If your website don't have this file, then find out which file is responsible for the syntax highlighting, or do the following.

1. Select the theme that you like from link abbove.

2. Copy the CSS file of theme (for exmaple `monokai.css`) to `your-blog-root-directory/css/` directory.

3. Open `your-blog-root-directory/css/main.css` file and add the `monokai.css` theme import:

```css
@import url(monokai.css);
```

But that’s not all. All of Pygments themes uses `.codehilite` as the default class. So we need to open for edit the CSS file of theme and replace all `.codehilite` with `.highlight` class.


### Using

When writing markdown with some code to be read by Jekyll, you can enable syntax highlighting with:

```
{% raw %}
{% highlight python %}
x = ('a', 1, False)
{% endhighlight %}
{% endraw %}
```

The argument to the `highlight` tag (`python` in the example above) is the language identifier. To find the appropriate identifier to use for the language you want to highlight, look for the “short name” on the [Rouge wiki](https://github.com/jayferd/rouge/wiki/List-of-supported-languages-and-lexers).

However, this becomes a bit verbose if you constantly switch between code and text.

By default, Jekyll sets the options for `fenced_code_blocks` to `true` which means you can define a code block with triple backticks. So just wrap your code with a triple backticks:

	```
	Some code.
	```

I recommend placing a blank line before and after code blocks to make the raw formatting easier to read.

You can also pass a language name to provide language specific highlighting:

	`​``javascript
	Some code.
	`​``

Note the `javascript` after the first pair of triple backticks. This is the language identifier. To find the appropriate identifier to use for the language you want to highlight, look for the “short name” on the [Rouge wiki](https://github.com/jayferd/rouge/wiki/List-of-supported-languages-and-lexers).
