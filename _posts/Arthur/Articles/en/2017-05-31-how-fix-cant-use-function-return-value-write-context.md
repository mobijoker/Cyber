---
title: 'How to fix: Can’t use function return value in write context'
ref: how-fix-cant-use-function-return-value-write-context
permalink: /web/how-fix-cant-use-function-return-value-write-context.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - how to fix
  - how fix
  - how to solve
  - solution
  - tutorial
  - wp error
  - wordpress error
  - error
  - issue
  - problem
  - function return value in write context

---

![thumb](/images/thumbnail/error.png)
After making an update to one of my WordPress plugins, when trying to load plugin settings page, I get the following error message:
<pre>
Fatal error: Can’t use function return value in write context in /public_html/domain-name.com/wp-content/plugins/rss-feed-icon-for-specificfeedscom/inc/php/functional.php on line 19
</pre>



### What causes this error

This error message is self explanatory. It means that we are trying to use function to return value in write context. It also tells us where exactly this error occurred. To solve this issue, follow the steps below.


### How to solve it

1. Open the file that is mentioned in the error message. In my case this is the `functional.php` file, which is placed in the `/public_html/domain-name.com/wp-content/plugins/rss-feed-icon-for-specificfeedscom/inc/php/` directory.

2. Find the line specified in the error message. In my case this is the 19th line.

3. Here you can see the code that causes the error. That's what it looks like in my case:

```php
if ( ! empty( get_option( 'my_option' ) ) {
```

> **Note!** You can see something similar to this but with `isset()` or another PHP function, and with custom function instead of WordPress function `get_option()`. For example:
>
>```php
>if ( ! empty( myFunction( $myVariable ) ) {
>```
>
> or:
> 
>```php
>if ( isset( $_POST( 'my_option' ) == TRUE ) ) {
>```

All I had to do to solve this error was to change the code above to the following:

```php
if ( ! get_option( 'my_option' ) )
```

This code does exactly the same thing but in more elegant way. Also we can make a variable and then use it in the our `if` construction:

```php
$my_option = get_option( 'my_option' );
if ( ! empty( $my_option ) {
```

Done! Now your plugin should work without this error.

Thanks for reading!
