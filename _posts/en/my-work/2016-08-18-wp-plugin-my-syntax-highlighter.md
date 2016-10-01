---
lang: en
ref: wp-plugin-my-syntax-highlighter
title: 'WP Plugin: "My Syntax Highlighter"'
author: Arthur Gareginyan
layout: post
permalink: /my_programs/wp-plugin-my-syntax-highlighter.html
categories:
  - Мои программы
  - my-work
tags:
  - plugin
  - wordpress
  - wp
  - code
  - php
  - html
  - css
  - javascript
  - js
  - xml
  - scss
  - less
  - sass
  - markdown
  - perl
  - sql
  - mysql
  - shell
  - bash
  - snippet
  - codemirror
  - hightlight
  - syntax highlighting
  - syntaxhighlighting
  - syntax highlighter
  - syntaxhighlighter
  - syntax
  - raw code
  - source code
  - shortcode

---

![thumb](/images/my-syntax-highlighter/icon.png)
Simple post syntax-highlighted code without losing it's formatting or making any manual changes. Supporting multiple languages, shortcodes and themes.

<br><br>

### Description

<img src="/images/my-syntax-highlighter/banner.png" alt="WP Plugin &quot;My Syntax Highlighter&quot;" />

An easy to use WordPress plugin that provides a simple way for embedding syntax-highlighted source code within pages or posts on your website, without losing it's formatting or making any manual changes. Supporting 14 languages, 16 shortcodes and 36 themes. The syntax highlighting feature implemented via a [CodeMirror](https://codemirror.net/) library.

Syntax highlighting is a feature that displays source code, in different colors and fonts according to the category of terms. Syntax highlighting is one strategy to improve the readability and context of the text; especially for code that spans several pages. The reader can easily ignore large sections of comments or code, depending on what they are looking for. 

This plugin also uses standalone Shortcode-Processor to prevent WordPress from converting newlines to HTML paragraphs, replacing apostrophes with typographic quotes and so on.

This plugin is just plug and play, no tedious configurations or hacks, just install, enable and start using your new shortcodes.


### Features

* Easy to use Settings Page
* Live preview on Settings Page
* Standalone Shortcode-Processor
* Syntax highlighting (by CodeMirror)
* Line numbering
* 36 Themes
* 14 Languages
* 16 Shortcodes
* Ready for translation (POT file included)
* Published on [WordPess.org](http://wordpess.org/)

**A list of supported languages:**

Click to view language examples. Highlighted with Default theme.

* [PHP](http://codemirror.net/mode/php/index.html)
* [JavaScript](http://codemirror.net/mode/javascript/index.html)
* [XML](http://codemirror.net/mode/xml/index.html)
* [HTML](http://codemirror.net/mode/htmlmixed/index.html)
* [CSS](http://codemirror.net/mode/css/index.html)
* [SCSS](http://codemirror.net/mode/css/scss.html)
* [LESS](http://codemirror.net/mode/css/less.html)
* [SASS](http://codemirror.net/mode/sass/index.html)
* [MarkDown](http://codemirror.net/mode/markdown/index.html)
* [Perl](http://codemirror.net/mode/perl/index.html)
* [SQL](http://codemirror.net/mode/sql/index.html)
* [MySQL](http://codemirror.net/mode/sql/index.html)
* [Shell](http://codemirror.net/mode/shell/index.html)
* [BASH](http://codemirror.net/mode/shell/index.html)


**A list of supported shortcodes:**

* [code][/code]
* [php][/php]
* [javascript][/javascript]
* [js][/js]
* [xml][/xml]
* [html][/html]
* [css][/css]
* [scss][/scss]
* [less][/less]
* [sass][/sass]
* [markdown][/markdown]
* [perl][/perl]
* [sql][/sql]
* [mysql][/mysql]
* [shell][/shell]
* [bash][/bash]


**A list of supported themes:**

* 3024-day
* 3024-night
* ambiance-mobile
* ambiance
* base16-dark
* base16-light
* blackboard
* cobalt
* colorforth
* eclipse
* elegant
* erlang-dark
* lesser-dark
* liquibyte
* mbo
* mdn-like
* midnight
* monokai
* neat
* neo
* night
* paraiso-dark
* paraiso-light
* pastel-on-dark
* rubyblue
* solarized
* the-matrix
* tomorrow-night-bright
* tomorrow-night-eighties
* ttcn
* twilight
* vibrant-ink
* xq-dark
* xq-light
* zenburn


### Screenshots

1. Plugin settings page.
<img src="/images/my-syntax-highlighter/screenshot-1.png" alt="WP plugin &quot;My Syntax Highlighter&quot; by Arthur Gareginyan" />
2. Example of post with added source code and wrapped it in shortcode provided by this plugin. Default theme of highlighter.
<img src="/images/my-syntax-highlighter/screenshot-2.png" alt="WP plugin &quot;My Syntax Highlighter&quot; by Arthur Gareginyan" />
3. Example of post with added source code and wrapped it in shortcode provided by this plugin. The "The Matrix" theme of highlighter.
<img src="/images/my-syntax-highlighter/screenshot-3.png" alt="WP plugin &quot;My Syntax Highlighter&quot; by Arthur Gareginyan" />
4. Example of post with added source codes on multiple language and wrapped it in shortcode provided by this plugin. Default theme of highlighter.
<img src="/images/my-syntax-highlighter/screenshot-4.png" alt="WP plugin &quot;My Syntax Highlighter&quot; by Arthur Gareginyan" />


### Quick-Start Guide

1. Upload "My Syntax Highlighter" to the `/wp-content/plugins/` directory.
2. Activate the plugin through the "Plugins" menu in WordPress.
3. Go to "Settings" -> "My Syntax Highlighter".


### Usage

Just switch to the Text/HTML editor and wrap your source code in one of the supported shortcodes (like `[code]...[/code]` that is universal shortcode) and this plugin takes care of the rest. Example:

```
[code]
This 

is 

an "example"!
[/code]
```

In this case, the shortcode will prevent WordPress from inserting paragraph breaks between `This`, `is` and `an "example"`, as well as ensure that the double quotes around `example` are not converted to typographic (curly) quotes.

To avoid problems, only edit posts that contain your source code in Text/HTML mode.


### Translation

This plugin is translate ready. But If your language is not available you can make one. The `.pot` file is included and placed in "languages" folder. Many of plugin users would be delighted if you shared your translation with the community. Just send the translation files (`*.po`, `*.mo`) to me at the arthurgareginyan@gmail.com and I will include the translation within the next plugin update.


### License

<img src="/images/gplv3.png" alt="gplv3" width="80" class="alignleft" />This plugin is open-sourced software licensed under the <a href="http://www.gnu.org/licenses/gpl-3.0.html" title="GPLv3" target="_blank">GNU General Public License, version 3 (GPLv3)</a> and is distributed free of charge.

Commercial licensing (e.g. for projects that can’t use an open-source license) is available upon request.


### Download

{% assign url = "https://downloads.wordpress.org/plugin/my-syntax-highlighter.zip" %}{% include button-wordpress.html %}
    
{% assign url = "https://github.com/ArthurGareginyan/my-syntax-highlighter" %}{% include button-github.html %}


<br>

>**Contribution**
>
>Developing plugins is long and tedious work. If you benefit or enjoy this plugin please take the time to:
>
>* [Donate](http://www.arthurgareginyan.com/donate.html) to support ongoing development. Your contribution would be greatly appreciated.
>* [Rate and Review](https://wordpress.org/support/view/plugin-reviews/my-syntax-highlighter?rate=5#postform) this plugin.
>* [Share with me](mailto:arthurgareginyan@gmail.com) or view the [GitHub Repo](https://github.com/ArthurGareginyan/my-syntax-highlighter) if you have any ideas or suggestions to make this plugin better.