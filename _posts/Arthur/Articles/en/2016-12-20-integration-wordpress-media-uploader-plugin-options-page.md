---
title: 'Integration of the WordPress Media Uploader into Plugin Options Page'
ref: integration-wordpress-media-uploader-plugin-options-page
permalink: /integration-wordpress-media-uploader-plugin-options-page.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - development
tags:
  - wordpress
  - plugin
  - plug-in
  - plugin creation
  - wordpress plugin
  - options page
  - wordpress options page
  - media uploader
  - wordpress media uploader
  - image uploader
  - wordpress image uploader
  - picture uploader
  - wordpress picture uploader
  - wordpress uploader 

---

![thumb](/images/integration-wordpress-media-uploader-plugin-options-page/1.png)
Sometimes I want to create a simple and intuitive graphic interface for my clients in order to give them an opportunity to upload an images on the options page of my plugin. I could make just a text input field where they can place the image URL, and sometimes it's what I need in a certain situation, but more often it is a not professional to make so. I want to have a happy clients, I want to make a user-friendly interface of my plugins. In this article I will show you how to integrate a beautiful, simple and customizable WordPress Media Uploader into your plugin options page.


<br><br>

**Note:** This tutorial is focused on uploading images to a plugin options page, so if you are not quite sure about how to create one, I recommend you first of all, have a look at the WordPress Settings API tutorials.


## What we will do and what we will get?

![](/images/integration-wordpress-media-uploader-plugin-options-page/1.png)

* We will add a button to our form to upload images to our server file system and another button to delete this image.

* We will create a field to preview the image. The user always needs to watch things happening on the screen. It is not enough for the user to upload an image and go to the page to check that the image is there.

* We will use the WordPress Media Uploader to upload the image or to pick an existing one so we will not have to worry about the whole process. We will also manage to upload the image to the right folder and we will attach it to the WordPress Media Library.

* We will be able to delete the image itself as well as its WordPress Media Library attachment.



## Demonstration

As an example I use the options page of one of my plugins. Here is how the button looks like on settings page of my WP plugin [RSS Fees Icon](https://wordpress.org/plugins/rss-feed-icon/):

![](/images/integration-wordpress-media-uploader-plugin-options-page/2.png)

**Note:** You can stylize it as you want by using CSS.

If you click on the "Upload" button, the WordPress media uploader popup window will appear.

![](/images/integration-wordpress-media-uploader-plugin-options-page/3.png)
![](/images/integration-wordpress-media-uploader-plugin-options-page/4.png)

In this window you can choose one of the previous uploaded images or upload a new one. Click on the "Insert into post" button and we will see this:

![](/images/integration-wordpress-media-uploader-plugin-options-page/5.png)

Now, we are already able to submit the form and save the image URL in the database.



## Tutorial

It is time to create our plugin options page, create a form on it and add it to the Admin Panel. As I have said before, the target of this tutorial is not to describe how to create a plugin options page, so I are not going to explain how to do it.


### Step 1. PHP code

We are going to create a PHP function (we will call it `arthur_image_uploader`) that will dynamically build HTML code for the Media Uploader:


```php
/**
 * Image Uploader
 * 
 * author: Arthur Gareginyan www.arthurgareginyan.com
 */
function arthur_image_uploader( $name, $width, $height ) {

    // Set variables
    $options = get_option( 'RssFeedIcon_settings' );
    $default_image = plugins_url('img/no-image.png', __FILE__);

    if ( !empty( $options[$name] ) ) {
        $image_attributes = wp_get_attachment_image_src( $options[$name], array( $width, $height ) );
        $src = $image_attributes[0];
        $value = $options[$name];
    } else {
        $src = $default_image;
        $value = '';
    }

    $text = __( 'Upload', RSSFI_TEXT );

    // Print HTML field
    echo '
        <div class="upload">
            <img data-src="' . $default_image . '" src="' . $src . '" width="' . $width . 'px" height="' . $height . 'px" />
            <div>
                <input type="hidden" name="RssFeedIcon_settings[' . $name . ']" id="RssFeedIcon_settings[' . $name . ']" value="' . $value . '" />
                <button type="submit" class="upload_image_button button">' . $text . '</button>
                <button type="submit" class="remove_image_button button">&times;</button>
            </div>
        </div>
    ';
}
```

**Note:** You can change the URL of an image that will be displayed by default (the 10th line, `$default_image` variable).

**Note:** Change the name of setting to your own (the 9th and 30th line, `RssFeedIcon_settings `). In this example I use setting in wich I save the array instead of just one value.

Place this function in the main PHP file of your plugin. Then only remains to use it on the plugin options page. Just call this function with some values from inside the form:

```
arthur_image_uploader( 'custom_image', $width = 115, $height = 115 );
```

**Note:** `custom_icon` - Is a name of your option that will be saved in the MySQL database.



### Step 2. jQuery code

Now we need some jQuery code in order to make the Media Uploader work properly. For this just place the following jQuery code in the JavaScript file of your plugin.

```js
// The "Upload" button
$('.upload_image_button').click(function() {
	var send_attachment_bkp = wp.media.editor.send.attachment;
	var button = $(this);
	wp.media.editor.send.attachment = function(props, attachment) {
		$(button).parent().prev().attr('src', attachment.url);
		$(button).prev().val(attachment.id);
		wp.media.editor.send.attachment = send_attachment_bkp;
	}
	wp.media.editor.open(button);
	return false;
});

// The "Remove" button (remove the value from input type='hidden')
$('.remove_image_button').click(function() {
	var answer = confirm('Are you sure?');
	if (answer == true) {
		var src = $(this).parent().prev().attr('data-src');
		$(this).parent().prev().attr('src', src);
		$(this).prev().prev().val('');
	}
	return false;
});
```

**Note:** If your plugin do not have the JavaScript file, create an empty `admin.js` file in your plugin folder and enqueue it into your plugin options page by using `wp_enqueue_script()` from the main PHP file of your plugin. Then place the above jQuery code in this JavaScript file.


That’s it. Now we can use the WordPress Media Uploader in our plugin options page.

If you have a question or you have any suggestions for improvement, please leave it in comments.
