---
lang: en
ref: loading-scripts-on-wordpress-admin-pages
title: Loading scripts on WordPress admin pages
date: 2015-10-16
author: Arthur Gareginyan
layout: post
permalink: /web/loading-scripts-on-wordpress-admin-pages.html
categories:
  - Web
tags:
  - action hook
  - admin_enqueue_scripts
  - certain admin page
  - cms wordpress
  - enqueue
  - hook
  - load
  - loading
  - plugin
  - register
  - script
  - scripts
  - settings page
  - specific admin page
  - wordpress
  - wp_enqueue_scripts

---

![thumb](/images/thumbnail/wordpress.png)
Sometimes you may want to create a separate style sheet and/or JavaScript file for settings page of your plugin, versus inserting it into existing code of this page. But how load this script on only a plugin’s or theme’s settings page (on certain `/wp-admin` pages)?


To load a style sheet and/or JavaScript file in the head section (header) of admin page/s we can use the `admin_enqueue_scripts` or the `wp_enqueue_scripts` action hook.

Depending on the purpose, you can load scripts on all pages of the web-site, on all pages of the Admin Panel or on a specific page of Admin Panel.

**1.** Load scripts everywhere on your website:

```php
function enqueue_my_scripts() {
 
    // ENQUEUE SCRIPTS…
 
}
add_action( 'wp_enqueue_scripts', 'enqueue_my_scripts' );
```

**2.** Load scripts on all Admin Panel pages:

```php
function enqueue_my_scripts() {
 
    // ENQUEUE SCRIPTS…
 
}
add_action( 'admin_enqueue_scripts', 'enqueue_my_scripts' );
```

**3.** Load scripts on a specific page of the top level menu in Admin Panel (in example `edit.php` - “Posts”):

```php
function enqueue_my_scripts($hook) {
    if ( 'edit.php' != $hook ) {
        return;
    }
 
    // ENQUEUE SCRIPTS…
 
}
add_action( 'admin_enqueue_scripts', 'enqueue_my_scripts' );
```

**4.** Load scripts on a specific page of the sub menu in Admin Panel.

Example:

```php
function enqueue_my_scripts($hook) {
    if ( 'appearance_page_my-page' != $hook ) {
        return;
    }
 
    // ENQUEUE SCRIPTS…
 
}
add_action( 'admin_enqueue_scripts', 'enqueue_my_scripts' );
```

In this example are uses the settings page that located in a sub menu of the “Appearance” section of menu and this page have the menu-slug `my-page`.

For use this method you need to identify the name of page. The page name which seen in the address bar is not valid for this.

The name of the page in “Appearance” section can be identified by the following scheme:

<pre>
themes.php?page={page menu-slug}
=>
appearance_page_{page menu-slug}
</pre>

The `appearance_page_` is a prefix for pages in this section of menu. You need to add the prefix to menu-slug. So, if the address to page you want is `themes.php?page=my-page.php`, then the name will be `appearance_page_my-page`. With other sections of Admin Panel do the same, but with different prefix. For “Settings” section of menu the prefix is `settings_page_`. If you can’t find the correct name of your plugin’s page then make do the follow.

Temporary add this function to your plugin's main file:

```php
function enqueue_my_scripts($hook) {
    echo "<p style='text-align:center;'>" .$hook. "</p>";
}
add_action('admin_enqueue_scripts', 'enqueue_my_scripts');
```

After that you’ll see a text line under top admin bar. There will be written the correct name of your plugin’s page. You can copy it and then delete this function.
