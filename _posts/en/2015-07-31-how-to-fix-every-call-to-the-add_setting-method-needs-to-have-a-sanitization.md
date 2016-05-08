---
id: 666
lang: en
ref: how-to-fix-every-call-to-the-add_setting-method-needs-to-have-a-sanitization
title: 'How to fix: "Every call to the add_setting() method needs to have a sanitization"'
date: 2015-07-31T05:09:29+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=666
permalink: /web/how-to-fix-every-call-to-the-add_setting-method-needs-to-have-a-sanitization.html
switch_like_status:
  - 1
categories:
  - Error
  - Web
tags:
  - add_setting
  - error
  - plugin
  - required
  - sanitiz
  - sanitization
  - sanitization callback function
  - theme
  - theme check
  - theme update
  - wordpress
  - wp

---

![thumb](/images/error-2-e1423133289573.png)
Some time ago WordPress.org is changed the rules of the publication of a themes to their repository. And then, I have not been able to publish update of my theme, because of the following error:


<pre>
REQUIRED: Found a Customizer setting that did not have a sanitization callback function. Every call to the add_setting() method needs to have a sanitization callback function passed.
</pre>

To localize the problem I used the <a href="https://wordpress.org/plugins/theme-check/" target="_blank">plugin "Theme Check"</a>. After installation plugins page will be located at `"WordPress Dashbord" -> "Appearance" -> "Theme Check"`. That plugin doesn't show more information than at wordpress.org when you publish an update of theme. But we can modify it, so let's start.

If the <a href="https://wordpress.org/plugins/theme-check/" target="_blank">"Theme Check" plugin</a> is not yet installed then do this.

Then modify `customizer.php` file which is located at `plugins/theme-check/checks/`. You can modify it directly out of your WordPress Dashbord. For this go to `"WordPress Dashbord" -> "Plugins" -> "Editor"` and select `"Theme Check"` plugin.

Now, in the file `customizer.php`, add this:

```
echo "$file_path: $match ";
```

After this section of code:

```
if ( false === strpos( $match, 'sanitize_callback' ) && false === strpos( $match, 'sanitize_js_callback' ) ) {
$this->error[] = '<span class="tc-lead tc-required">' . __('REQUIRED','theme-check') . '</span>: ' . __( 'Found a Customizer setting that did not have a sanitization callback function. Every call to the <strong>add_setting()</strong> method needs to have a sanitization callback function passed.', 'theme-check' );
```

Done. This should indicate the file and fragment of code that causing the error. In my case, it show this string:
<pre>
/var/www/site/wp-content/themes/anarcho-notepad/inc/customizer.php: 'copyright_post', array( 'default' => 'Copyright ©
</pre>

This string mean that code which causing the error is this:

<pre>
'copyright_post', array( 'default' => 'Copyright ©
</pre>

and it located in the file `customizer.php`. So I need to find this code in that file. There is:

```
// Copyright after post
$wp_customize->add_setting( 'copyright_post', array(
	'default'			=> 'Copyright &copy; 2014. All rights reserved.',
	'sanitize_callback'	=> 'esc_attr',
));
```

How you see the sanitize callback function is there. The cause was in the special character "&copy;" in the value of the key "default".

`&copy ; = Copyright = © = (c)`

Now I must replace the special character `&copy ;` to text version `(c)` or just remove it.
