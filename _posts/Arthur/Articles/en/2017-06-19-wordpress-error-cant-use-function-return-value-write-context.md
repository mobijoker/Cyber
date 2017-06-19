---
title: 'WordPress error: Can’t use function return value in write context'
ref: wordpress-error-cant-use-function-return-value-write-context
permalink: /web/wordpress-error-cant-use-function-return-value-write-context.html
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
  - wordpress problem 
  - wordpress issue
  - error
  - issue
  - problem
  - function return value in write context

---

![thumb](/images/thumbnail/error.png)
My WordPress website crashed after installing an update of one of the plugins. Then I could see only the white screen with the following error message:
<pre>
Fatal error: Can’t use function return value in write context in /public_html/domain-name.com/wp-content/plugins/some-plugin/inc/php/functional.php on line 19
</pre>


For developers, I recommend reading [another article](/web/how-fix-cant-use-function-return-value-write-context.html) about this error.


### What causes this error

This error message means that one of the plugins that installed on your WordPress website causes a fatal error. It also tells you which exactly plugin causes this error (You can find out this from the address given in the message. In my case is a plugin called the "some-plugin"). To solve this issue, follow the steps below.


### How to restore the website?

> **Note!** Never try to change the code of plugin or theme, this can lead to even greater problems. Leave code changes to professionals.

If you see this error message then most likely your website is down and you do not have access to the WordPress admin panel of your website. So a manual changes via FTP is needed in order to get back in to the WordPress admin panel. Since we know that the error is caused by the plugin and we know exactly which plugin, then we need to temporarily delete this plugin via FTP access to the files of our website in order to bring the website back to life. Then let's go!

1. Connect to your website via FTP access. This would require the FTP credentials from your web hosting provider.

2. Find the plugin folder under `/public-html/domain-name.com/wp-content/plugins/`.

3. Delete the whole folder of the plugin that mentioned in the error message. In my case is the folder with name `/some-plugin/`.

> **Note!** If you’re having issues with this, most hosting support can do this on their end for you.

Done! Now your website should be returned to life and the WordPress admin panel should be accessible.


### What to do with plugin?

Immediately contact with the developer of the plugin that caused an error and report him about the error with providing much information as possible. Once the developer will release an update of the plugin, you can reinstall the plugin, which should now be fixed.

Thanks for reading!
