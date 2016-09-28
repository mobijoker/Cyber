---
lang: en
ref: add-social-media-buttons-to-your-website
title: Add social media buttons to your website
date: 2015-09-06T15:23:50+00:00
author: Arthur Gareginyan
layout: post
permalink: /web/add-social-media-buttons-to-your-website.html
categories:
  - Web
tags:
  - button
  - icon
  - social media
  - social media buttons
  - social media icons
  - social media profile
  - social network
  - значки
  - значки социальных сетей
  - иконки
  - иконки социальных сетей
  - кнопки
  - кнопки социальных сетей
  - социальные медиа
  - социальные сети

---

![thumb](/images/social-media-buttons-toolbar/icon.png)
The social media buttons lets you add icons of the popular social networks which are linked to your social media profiles. You will learn how to add a vertical and horizontal line or lines of social media buttons to your website’s post, sidebar or footer, using whatever icons you prefer.


Here’s an example of what it looks like:
<img src="/images/social-media-buttons-toolbar/social-media-icons-2.png" alt="social media icons-2" width="600" height="206" class="aligncenter" />

Social Media Buttons Toolbar displayed below the content of a post (Twenty Sixteen theme) :
<img src="/images/social-media-buttons-toolbar/screenshot-4.png" alt="WP plugin &quot;Social Media Buttons Toolbar&quot; by Arthur Gareginyan" width="1024" height="541" />

Social Media Buttons Toolbar displayed in the sidebar using a shortcode in text widget (Twenty Sixteen theme) :
<img src="/images/social-media-buttons-toolbar/screenshot-5.png" alt="WP plugin &quot;Social Media Buttons Toolbar&quot; by Arthur Gareginyan" width="1024" height="541" />

Social Media Buttons Toolbar displayed in the footer using a simple call the function directly from theme file (vCard theme) :
<img src="/images/social-media-buttons-toolbar/screenshot-7.png" alt="WP plugin &quot;Social Media Buttons Toolbar&quot; by Arthur Gareginyan" width="1024" height="541" />

Social Media Buttons Toolbar displayed in the footer using a shortcode in text widget (Anarcho Notepad theme):
<img src="/images/social-media-buttons-toolbar/screenshot-6.png" alt="WP plugin &quot;Social Media Buttons Toolbar&quot; by Arthur Gareginyan" width="379" height="359" />

Buttons arranged horizontally and centered. If they do not fit to the one line, then they will be placed on multiple lines.

You can add social media buttons to your website or blog by two ways, but first you need an icons.

### Preparing

#### Finding, downloading and uploading icons to your website

**Step 1.** On the internet find the social media icons you would like to use. Make sure you’re not violating any copyright. Once you’ve found some that you like, download them to your computer.

I using <a href="https://www.iconfinder.com/iconsets/social-buttons-2?ref=ArthurGareginyan" target="_blank">“Social Buttons 2”</a> set of icons by Ivlichev Victor Petrovich. This set of icons is free and licensed under Creative Commons (Attribution 3.0 Unported).

**Step 2.** Put all icons in new folder, example `social-media-icons` and upload them to your website’s media library. In the CMS WordPress this is folder with name `uploads` (it located at `/you-website/wp-content/uploads/`). Then address to your icons will be similar to this:
`http://your-website.com/wp-content/uploads/social-media-icons/facebook.ico`


### The first way to add social media buttons

The first way to add social media buttons is a using Text Widget.

**Step 1.** Go to the your website’s admin panel. Add a Text Widget to your sidebar or footer.

**Step 2.** Add to the Text Widget the some HTML that is similar to below (I using this code):

```html
Follow me on social media:
<ul class="social-icons">
	<li>
		<a href="https://www.facebook.com/arthur.gareginyan" target='blank'>
			<img src="/images/social-media-icons/facebook.png" alt="Facebook" />
		</a>
	</li>
	<li>
		<a href="https://twitter.com/AGareginyan" target='blank'>
			<img src="/images/social-media-icons/twitter.png" alt="Twitter" />
		</a>
	</li>
	<li>
		<a href="http://instagram.com/arthur_gareginyan" target='blank'>
			<img src="/images/social-media-icons/instagram.png" alt="Instagram" />
		</a>
	</li>
	<li>
		<a href="https://plus.google.com/+ArthurGareginyan" target='blank'>
			<img src="//mycyberuniverse.com/wp-content/uploads/social-media-icons/google.png" alt="Google+" />
		</a>
	</li>
	<li>
		<a href="https://www.youtube.com/channel/UCvQenE1DumnZy1k5sTvgmSA" target='blank'>
			<img src="/images/social-media-icons/youtube.png" alt="YouTube" />
		</a>
	</li>
	<li>
		<a href="http://oneberserk.blogspot.ru" target='blank'>
			<img src="/images/social-media-icons/blogger.png" alt="Blogger" />
		</a>
	</li>
	<li>
		<a href="http://www.linkedin.com/in/arthurgareginyan" target='blank'>
			<img src="/images/social-media-icons/linkedin.png" alt="Linkedin" />
		</a>
	</li>
	<li>
		<a href="https://github.com/ArthurGareginyan" target='blank'>
			<img src="/images/social-media-icons/github.png" alt="Github" />
		</a>
	</li>
	<li>
		<a href="http://codepen.io/berserkr/" target='blank'>
			<img src="/images/social-media-icons/codepen.png" alt="Codepen" />
		</a>
	</li>
	<li>
		<a href="mailto:arthurgareginyan@gmail.com?subject=Message from mycyberuniverse.com" target='blank'>
			<img src="/images/social-media-icons/mail.png" alt="Mail" />
		</a>
	</li>
	<li>
		<a href="http://mycyberuniverse.com/feed" target='blank'>
			<img src="/images/social-media-icons/rss.png" alt="RSS Feed" />
		</a>
	</li>
</ul>
<style>
.social-icons {
    text-align: center;
}
.social-icons li {
    display:inline-block;
    list-style-type:none;
    -webkit-user-select:none;
    -moz-user-select:none;
}
.social-icons li a {
    border-bottom: none;
}
.social-icons li img {
    width:70px;
    height:70px;
    margin-right: 20px;
}
</style>
```

How you see the code above is composed of two parts. The first is a list with links to your social network profiles and your icons:

```html
<ul>
	<li>
		…
	</li>
</ul>
```

Replace all my links with your links that you want the button to point to. Make sure each link begins with `http://` or `https://`.

The second is a styles for your buttons:

```html
<style>
	…
</style>
```

Also you can use this method for display your social media buttons in the post.


### The second way to add social media buttons

The second way to add social media buttons is a creating the php function for display the buttons in any place of your website by using the shortcode. For this you need to manage `functions.php` file of your theme or use the <a href="https://wordpress.org/plugins/my-custom-functions/" target="_blank">plugin “My Custom Functions”</a>.

**Step 1.** We will use the same code as in the first way, but we close the code into a function. Add some HTML that is similar to below in `functions.php` file of your theme or in the plugin:

```php
/* SOCIAL MEDIA BUTTONS
************************************/
function my_social_media_icons(){
ob_start();
?>
</br>
Follow me on social media:
<ul class="social-icons">
	<li>
		<a href="https://www.facebook.com/arthur.gareginyan" target='blank'>
			<img src="/images/social-media-icons/facebook.png" alt="Facebook" />
		</a>
	</li>
	<li>
		<a href="https://twitter.com/AGareginyan" target='blank'>
			<img src="/images/social-media-icons/twitter.png" alt="Twitter" />
		</a>
	</li>
	<li>
		<a href="http://instagram.com/arthur_gareginyan" target='blank'>
			<img src="/images/social-media-icons/instagram.png" alt="Instagram" />
		</a>
	</li>
	<li>
		<a href="https://plus.google.com/+ArthurGareginyan" target='blank'>
			<img src="//mycyberuniverse.com/wp-content/uploads/social-media-icons/google.png" alt="Google+" />
		</a>
	</li>
	<li>
		<a href="https://www.youtube.com/channel/UCvQenE1DumnZy1k5sTvgmSA" target='blank'>
			<img src="/images/social-media-icons/youtube.png" alt="YouTube" />
		</a>
	</li>
	<li>
		<a href="http://oneberserk.blogspot.ru" target='blank'>
			<img src="/images/social-media-icons/blogger.png" alt="Blogger" />
		</a>
	</li>
	<li>
		<a href="http://www.linkedin.com/in/arthurgareginyan" target='blank'>
			<img src="/images/social-media-icons/linkedin.png" alt="Linkedin" />
		</a>
	</li>
	<li>
		<a href="https://github.com/ArthurGareginyan" target='blank'>
			<img src="/images/social-media-icons/github.png" alt="Github" />
		</a>
	</li>
	<li>
		<a href="http://codepen.io/berserkr/" target='blank'>
			<img src="/images/social-media-icons/codepen.png" alt="Codepen" />
		</a>
	</li>
	<li>
		<a href="mailto:arthurgareginyan@gmail.com?subject=Message from mycyberuniverse.com" target='blank'>
			<img src="/images/social-media-icons/mail.png" alt="Mail" />
		</a>
	</li>
	<li>
		<a href="http://mycyberuniverse.com/feed" target='blank'>
			<img src="/images/social-media-icons/rss.png" alt="RSS Feed" />
		</a>
	</li>
</ul>
<style>
.social-icons {
    text-align: center;
}
.social-icons li {
    display:inline-block;
    list-style-type:none;
    -webkit-user-select:none;
    -moz-user-select:none;
}
.social-icons li a {
    border-bottom: none;
}
.social-icons li img {
    width:70px;
    height:70px;
    margin-right: 20px;
}
</style>
</br>
<?php
$output = ob_get_clean();
return $output;
}
add_shortcode('my_social_media_icons', 'my_social_media_icons'); // Create shortcode
add_filter('widget_text', 'do_shortcode');  // Allow shortcodes in widgets
```

* The string `add_shortcode(` are creates the shortcode `[my_social_media_icons]`.
* The string `add_filter(` is needed to allow the shortcodes in widgets.

And now you can use the shortcode `[my_social_media_icons]`. Just put this shortcode in any place of your website, like post, sidebar or footer and your social media buttons will be displayed.

**P.S.**
If you use any other CMS instead of WordPress then you must remove the string with creating shortcode and filter:

```php
add_shortcode('my_social_media_icons', ‘my_social_media_icons');
add_filter('widget_text', 'do_shortcode');
```

Instead of using shortcode you must use below code to display the buttons:

```html
<?php my_social_media_icons(); ?>
```
