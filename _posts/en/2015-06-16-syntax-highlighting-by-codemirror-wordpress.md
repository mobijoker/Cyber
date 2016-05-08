---
id: 641
lang: en
ref: syntax-highlighting-by-codemirror-wordpress
title: 'Syntax highlighting by CodeMirror &#038; WordPress'
date: 2015-06-16T22:41:35+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=641
permalink: /web/syntax-highlighting-by-codemirror-wordpress.html
switch_like_status:
  - 1
categories:
  - Web
tags:
  - codemirror
  - highlight
  - highlighter
  - highlighting
  - javascript
  - syntax
  - wordpress
  - подсветка кода
  - подсветка синтаксиса

---

![thumb](/images/CodeMirror.png)
About using of JavaScript library CodeMirror together with CMS WordPress and its integration into WordPress projects (themes and plugins).


CodeMirror is a JavaScript component that provides a code editor in the browser. When a mode is available for the language you are coding in, it will color your code (syntax highlighting), and optionally help with indentation.


### Building a package CodeMirror

At the beginning you need to build a catalog of CodeMirror with the needed modules, and addons and themes if necessary. This can be done simply. Just download the archive with CodeMirror from the developer website (<a href="http://codemirror.net" target="_blank">http://codemirror.net</a>) and removing of unnecessary leave just the needed.

The minimum required package:

* Catalog `lib` with the files `codemirror.js` and `codemirror.css`.
* Catalog `mode` with needed modes (only js files).
* Catalogs `theme` and `addon` needs only if use theme or addons.
* If you want to publish your project, then you need to use the `LICENSE` and `README.md` files.

I give an example of the syntax highlighting of HTML and PHP languages. The needed modes you can specify on [this page](https://codemirror.net/mode/) of the Manual.

And need another two files (`config.js`, `customestyle.css`) which I will tell later.

Now all of this must be placed in a directory with the name `codemirror` at the root of the project. As a result, the builded directory should look something like this:

<pre>
codemirror-.
           |--lib--.
           |       |--codemirror.js
           |       '--codemirror.css
           |
           |--mode-.
           |       |--xml.js
           |       |--javascript.js
           |       |--css.js
           |       |--htmlmixed.js
           |       |--clike.js
           |       '--php.js
           |
           |--theme-.
           |        '--default.css
           |
           |--addon-.
           |        '--
           |
           |--LICENSE
           |--README.md
           |--config.js
           '--customestyle.css
</pre>


### Loading the scripts of CodeMirror

You must load CodeMirror scripts (those created in previous paragraph) in the header of the page/s. To do this in WordPress there is a special function `_enqueue_scripts` that load scripts and styles in the header of pages.

Example of loading the scripts with registration:

```
/**
 * Register and enqueue the CodeMirror scripts and styles
 */
function enqueue_codemirror_scripts($hook) {

    if ( 'appearance_page_my-custom-functions' != $hook ) {
        return;
    }

    // Registering scripts
    wp_register_script('codemirror', plugin_dir_url(__FILE__) . 'codemirror/lib/codemirror.js');
    wp_register_script('codemirror_xml', plugin_dir_url(__FILE__) . 'codemirror/mode/xml.js');
    wp_register_script('codemirror_javascript', plugin_dir_url(__FILE__) . 'codemirror/mode/javascript.js');
    wp_register_script('codemirror_css', plugin_dir_url(__FILE__) . 'codemirror/mode/css.js');
    wp_register_script('codemirror_htmlmixed', plugin_dir_url(__FILE__) . 'codemirror/mode/htmlmixed.js');
    wp_register_script('codemirror_clike', plugin_dir_url(__FILE__) . 'codemirror/mode/clike.js');
    wp_register_script('codemirror_php', plugin_dir_url(__FILE__) . 'codemirror/mode/php.js');
    wp_register_script('codemirror_config', plugin_dir_url(__FILE__) . 'codemirror/config.js');
    wp_register_style('codemirror_style', plugin_dir_url(__FILE__) . 'codemirror/lib/codemirror.css');
    wp_register_style('codemirror_customestyle', plugin_dir_url(__FILE__) . 'codemirror/customestyle.css');

    // Enqueue scripts
    wp_enqueue_script('codemirror');
    wp_enqueue_script('codemirror_xml');
    wp_enqueue_script('codemirror_javascript');
    wp_enqueue_script('codemirror_css');
    wp_enqueue_script('codemirror_htmlmixed');
    wp_enqueue_script('codemirror_clike');
    wp_enqueue_script('codemirror_php');
    wp_enqueue_script('codemirror_config');
    wp_enqueue_style('codemirror_style');
    wp_enqueue_style('codemirror_customestyle');

}
add_action( 'admin_enqueue_scripts', 'enqueue_codemirror_scripts' );
```

And without registration (if there is no need for registration):
```
/**
 * Enqueue the CodeMirror scripts and styles
 */
function enqueue_codemirror_scripts($hook) {
    if ( 'appearance_page_my-custom-functions' != $hook ) {
        return;
    }

    wp_enqueue_script('codemirror', plugin_dir_url(__FILE__) . 'codemirror/lib/codemirror.js');
    wp_enqueue_script('codemirror_xml', plugin_dir_url(__FILE__) . 'codemirror/mode/xml.js');
    wp_enqueue_script('codemirror_javascript', plugin_dir_url(__FILE__) . 'codemirror/mode/javascript.js');
    wp_enqueue_script('codemirror_css', plugin_dir_url(__FILE__) . 'codemirror/mode/css.js');
    wp_enqueue_script('codemirror_htmlmixed', plugin_dir_url(__FILE__) . 'codemirror/mode/htmlmixed.js');
    wp_enqueue_script('codemirror_clike', plugin_dir_url(__FILE__) . 'codemirror/mode/clike.js');
    wp_enqueue_script('codemirror_php', plugin_dir_url(__FILE__) . 'codemirror/mode/php.js');
    wp_enqueue_script('codemirror_php', plugin_dir_url(__FILE__) . 'codemirror/config.js');
    wp_enqueue_style('codemirror_style', plugin_dir_url(__FILE__) . 'codemirror/lib/codemirror.css');
    wp_enqueue_style('codemirror_style', plugin_dir_url(__FILE__) . 'codemirror/customestyle.css');

}
add_action( 'admin_enqueue_scripts', 'enqueue_codemirror_scripts' );
```

For plugin paths to scripts specified using `plugin_dir_url()`:

```
wp_enqueue_script( 'my_custom_script', plugin_dir_url( __FILE__ ) . 'myscript.js' );
```

And for themes with the `get_template_directory_uri()`:

```
wp_enqueue_script( 'my_custom_script', get_template_directory_uri( __FILE__ ) . 'myscript.js' );
```

**Note:** `myscript.is` - is the name of the needed file.

Depending on the purpose, you can load scripts on all pages of the website, on all pages of the Admin Panel or on a certain page.

Load scripts on all pages of website:

```
function enqueue_codemirror_scripts() {

    // Enqueue scripts
    ...

}
add_action( 'wp_enqueue_scripts', 'enqueue_codemirror_scripts' );
```

Load scripts on all Admin pages:

```
function enqueue_codemirror_scripts() {

    // Enqueue scripts
    ...

}
add_action( 'admin_enqueue_scripts', 'enqueue_codemirror_scripts' );
```

Load scripts on a specific Admin page (in my example is edit.php): 

```
function enqueue_codemirror_scripts($hook) {
    if ( 'edit.php' != $hook ) {
        return;
    }

    // Enqueue scripts
    ...

}
add_action( 'admin_enqueue_scripts', 'enqueue_codemirror_scripts' );
```

**Note:** The page title can be seen in the address bar.

But if you need a page of theme then it will be a little harder.

The name of the page of theme can be identified by the following scheme:

<pre>
themes.php?page={page}
=>
appearance_page_{page}
</pre>

If the address of the page you want:

<pre>
themes.php?page=my-page.php
</pre>

The title will be `appearance_page_my-page`.


### Settings

All configuration of CodeMirror is made from the config file `config.js`. You must create this file and put into it the following contents:

```
// Configuration file for CodeMirror v1.0

  var myCodeMirror = CodeMirror.fromTextArea(document.getElementById('CodeMirror'), {
     lineNumbers: true,
     matchBrackets: true,
     mode: 'application/x-httpd-php',
     indentUnit: 4
  });
```

**Note:** Use the syntax JavaScript.

The settings are specified as options of variable `myCodeMirror`.

Option values from my example:

<pre>
lineNumbers: true, 				// Show line numbers.
matchBrackets: true,				// Highlights paired brace.
mode: "application/x-httpd-php",		// Mode of the highlight.
indentUnit: 4 					// Tab size.
</pre>

The remaining options can be found on the page of the Manual:
<a href="https://codemirror.net/doc/manual.html#config" target="_blank">https://codemirror.net/doc/manual.html#config</a>

**Note:** Line with the options, except the last must end with a comma.


### Styles

To apply your own styles you need to create the file `customestyle.css`.

An example of the contents of a file `customestyle.css`:

```
  .CodeMirror {
     border: 1px solid cornflowerblue;
     height: auto;
  }
```

**Note:** Use the syntax CSS.


### Processed field

Now the last paragraph. You must specify the CodeMirror area for handling code. This is done using the HTML tag `<textarea>` (text box) with `id` - `CodeMirror`. On needed pages, highlighted code need to wrap in this tag, like so:

```
<textarea cols="50" rows="10" id="CodeMirror" >
</textarea>
```


### Epilogue

If all the code put on one HTML page it will look like this:

```
...
   <script src="codemirror/lib/codemirror.js"></script>
   <script src="codemirror/mode/xml.js"></script>
   <script src="codemirror/mode/javascript.js"></script>
   <script src="codemirror/mode/css.js"></script>
   <script src="codemirror/mode/htmlmixed.js"></script>
   <script src="codemirror/mode/clike.js"></script>
   <script src="codemirror/mode/php.js"></script>
   <link rel="stylesheet" href="codemirror/lib/codemirror.css">
   <link rel="stylesheet" href="codemirror/theme/default.css">
</head>
<body>
   <div id="container">
      <textarea cols="50" rows="10" id="code" ></textarea>
   </div>
   <script type="text/javascript" language="javascript">
     var myCodeMirror = CodeMirror.fromTextArea(document.getElementById('code'), {
        lineNumbers: true,
        matchBrackets: true,
        mode: 'application/x-httpd-php',
        indentUnit: 4
     });
   </script>
   <style>
     .CodeMirror {
        border: 1px solid cornflowerblue;
        height: auto;
     }
   </style>
</body>
</html>
…
```


### Links

* Official website:
<a href="http://codemirror.net" target="_blank">http://codemirror.net</a>
* Official Manual:
<a href="http://codemirror.net/doc/manual.html" target="_blank">http://codemirror.net/doc/manual.html</a>
* Page on the GitHub:
<a href="https://github.com/codemirror/codemirror" target="_blank">https://github.com/codemirror/codemirror</a>
