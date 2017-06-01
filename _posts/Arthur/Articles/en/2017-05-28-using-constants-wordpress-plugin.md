---
title: 'Using constants in WordPress plugin'
ref: using-constants-wordpress-plugin
permalink: /web/using-constants-wordpress-plugin.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - how to fix
  - tutorial
  - wordpress
  - wp
  - wordpress plugin
  - wp plugin
  - constant
  - php constant
  - wordpress constant
  - wp constant

---

![thumb](/images/thumbnail/wordpress.png)
I've been writing WordPress plugins for a long time. At the top of the main plugin file, I usually define some constants. These constants contain basic information about my plugin, such as: Name of plugin, Path to plugin folder, Text domain name, and etc. Constants give me the opportunity to have easy and quick access to this information. And if I need to change any of this information, then I just change it once in constant instead of looking for every mention of this information in all plugin files.

> **Note!** The following examples of code are taken from my WordPress plugin ["All Meta Tags"](https://wordpress.org/plugins/all-meta-tags/). `ALLMT` will be a constants prefix. Constants will have the following value:
> 
> * `ALLMT_DIR` - `dirname( plugin_basename( __FILE__ ) )`
> * `ALLMT_BASE` - `plugin_basename( __FILE__ )`
> * `ALLMT_URL` - `plugin_dir_url( __FILE__ )`
> * `ALLMT_PATH` - `plugin_dir_path( __FILE__ )`
> * `ALLMT_SLUG` - `dirname( plugin_basename( __FILE__ ) )`
> * `ALLMT_NAME` - `All Meta Tags`
> * `ALLMT_VERSION` - `4.1.1`
> * `ALLMT_TEXT` - `all-meta-tags`
> * `ALLMT_PREFIX` - `allmetatags`
> * `ALLMT_SETTINGS` - `allmetatags`
> 
> Some of these values is get by using WordPress API.

Just a few lines of code are enough and I can work with constants:

```php
// Define global constants
if ( !defined( 'ALLMT_DIR' ) ) {
	define( 'ALLMT_DIR', dirname( plugin_basename( __FILE__ ) ) );
}
if ( !defined( 'ALLMT_BASE' ) ) {
	define( 'ALLMT_BASE', plugin_basename( __FILE__ ) );
}
if ( !defined( 'ALLMT_URL' ) ) {
	define( 'ALLMT_URL', plugin_dir_url( __FILE__ ) );
}
if ( !defined( 'ALLMT_PATH' ) ) {
	define( 'ALLMT_PATH', plugin_dir_path( __FILE__ ) );
}
if ( !defined( 'ALLMT_SLUG' ) ) {
	define( 'ALLMT_SLUG', dirname( plugin_basename( __FILE__ ) ) );
}
if ( !defined( 'ALLMT_NAME' ) ) {
	define( 'ALLMT_NAME', 'All Meta Tags' );
}
if ( !defined( 'ALLMT_VERSION' ) ) {
	define( 'ALLMT_VERSION', '4.1.1' );
}
if ( !defined( 'ALLMT_TEXT' ) ) {
	define( 'ALLMT_TEXT', 'all-meta-tags' );
}
if ( !defined( 'ALLMT_PREFIX' ) ) {
	define( 'ALLMT_PREFIX', 'allmetatags' );
}
if ( !defined( 'ALLMT_SETTINGS' ) ) {
	define( 'ALLMT_SETTINGS', 'allmetatags' );
}
```

It's that simple. But I think that it is difficult to read, so for code readability, I consider using the following one-liner code (although you could put a regular `if` construction on a single line as well):

```php
// Define global constants
defined( 'ALLMT_DIR' ) or define( 'ALLMT_DIR', dirname( plugin_basename( __FILE__ ) ) );
defined( 'ALLMT_BASE' ) or define( 'ALLMT_BASE', plugin_basename( __FILE__ ) );
defined( 'ALLMT_URL' ) or define( 'ALLMT_URL', plugin_dir_url( __FILE__ ) );
defined( 'ALLMT_PATH' ) or define( 'ALLMT_PATH', plugin_dir_path( __FILE__ ) );
defined( 'ALLMT_SLUG' ) or define( 'ALLMT_SLUG', dirname( plugin_basename( __FILE__ ) ) );
defined( 'ALLMT_NAME' ) or define( 'ALLMT_NAME', 'All Meta Tags' );
defined( 'ALLMT_VERSION' ) or define( 'ALLMT_VERSION', '4.1.1' );
defined( 'ALLMT_TEXT' ) or define( 'ALLMT_TEXT', 'all-meta-tags' );
defined( 'ALLMT_PREFIX' ) or define( 'ALLMT_PREFIX', 'allmetatags' );
defined( 'ALLMT_SETTINGS' ) or define( 'ALLMT_SETTINGS', 'allmetatags' );
```

I used this solution quite a long time. Then I wanted to add a variable with constants prefix for a more universal solution since I have a lot of plugins in which I want to use constants. Also I wanted to use some plugin meta-data from the plugin header (information that placed in the comment section at the beginning of the main plugin file). This will be helpful when changing the plugin version in the comments, so I don't need to remember to change it in the constant. For this I will use the `get_file_data()` function.

```php
// Define global constants
$constant_name_prefix = 'ALLMT_';
$plugin_data = get_file_data( __FILE__, array( 'name'=>'Plugin Name', 'version'=>'Version', 'text'=>'Text Domain' ) );
defined( $constant_name_prefix . 'DIR' ) or define( $constant_name_prefix . 'DIR', dirname( plugin_basename( __FILE__ ) ) );
defined( $constant_name_prefix . 'BASE' ) or define( $constant_name_prefix . 'BASE', plugin_basename( __FILE__ ) );
defined( $constant_name_prefix . 'URL' ) or define( $constant_name_prefix . 'URL', plugin_dir_url( __FILE__ ) );
defined( $constant_name_prefix . 'PATH' ) or define( $constant_name_prefix . 'PATH', plugin_dir_path( __FILE__ ) );
defined( $constant_name_prefix . 'SLUG' ) or define( $constant_name_prefix . 'SLUG', dirname( plugin_basename( __FILE__ ) ) );
defined( $constant_name_prefix . 'NAME' ) or define( $constant_name_prefix . 'NAME', $plugin_data['name'] );
defined( $constant_name_prefix . 'VERSION' ) or define( $constant_name_prefix . 'VERSION', $plugin_data['version'] );
defined( $constant_name_prefix . 'TEXT' ) or define( $constant_name_prefix . 'TEXT', $plugin_data['text'] );
defined( $constant_name_prefix . 'PREFIX' ) or define( $constant_name_prefix . 'PREFIX', 'allmetatags' );
defined( $constant_name_prefix . 'SETTINGS' ) or define( $constant_name_prefix . 'SETTINGS', 'allmetatags' );
```

> **Note!** By using `get_file_data()` function we can get meta-data and put it in the array (in the example above is `$plugin_data`). Then we can get, for example the plugin version, with the `$plugin_data['version']`.


This method I found interesting, but it is still difficult to read, so I continued to search for a better solution. Then I thought about using a custom function to generate constants and that's what I got:

```php
// Define global constants
$plugin_data = get_file_data( __FILE__, array( 'name'=>'Plugin Name', 'version'=>'Version', 'text'=>'Text Domain' ) );
function allmetatags_constants( $constant_name, $value ) {
    $constant_name_prefix = 'ALLMT_';
    $constant_name = $constant_name_prefix . $constant_name;
    if ( !defined( $constant_name ) )
        define( $constant_name, $value );
}
allmetatags_constants( 'DIR', dirname( plugin_basename( __FILE__ ) ) );
allmetatags_constants( 'BASE', plugin_basename( __FILE__ ) );
allmetatags_constants( 'URL', plugin_dir_url( __FILE__ ) );
allmetatags_constants( 'PATH', plugin_dir_path( __FILE__ ) );
allmetatags_constants( 'SLUG', dirname( plugin_basename( __FILE__ ) ) );
allmetatags_constants( 'NAME', $plugin_data['name'] );
allmetatags_constants( 'VERSION', $plugin_data['version'] );
allmetatags_constants( 'TEXT', $plugin_data['text'] );
allmetatags_constants( 'PREFIX', 'allmetatags' );
allmetatags_constants( 'SETTINGS', 'allmetatags' );
```

> * First parameter of function is name of global constant.
> * Second parameter of function is value of global constant.

> **Note!** To use this in your WordPress plugin, be sure to replace the function prefix "allmetatags" and the constants prefix "ALLMT" with your own ones.

This is much nicer to read, isn't it?



### Summarizing

This way I use PHP constants in all of my WordPress plugins. This method is compatible with PHP versions from 5.2 to 7.0.

If you were able to implement this on your WordPress plugin then please leave a comment.

Thanks for reading!