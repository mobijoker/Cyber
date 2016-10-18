---
title: Adding an email subscription button to your blog by using Feedburner
ref: adding-email-subscription-button-blog-using-feedburner
permalink: /web/adding-email-subscription-button-blog-using-feedburner.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - feedburner
  - subscribe button
  - subscription
  - subscribe
  - email subscription

---

![thumb](/images/adding-email-subscription-button-blog-using-feedburner/rss-feed.png)
A great way to keep up to date with a blog that you love to follow is to subscribe to an email subscription of their posts. That way, when a new post is made, it lands right in your email inbox. If you want to offer this to people who visit your blog, it is easy to do. In this article I show you how to add to your blog an email subscription button that connected to Feedburner.

<br>

Feedburner is a feed management webapp. Currently owned by Google but not supported by Google anymore. If you setup your website feed in Feedburner, it will modify the feed according to your requirement. It also provides traffic stats and other useful statistics. The majority of blogging community is using Feedburner for its subscribe option.

Now, step by step guide.


## **Step 1.** Find the RSS feed

First of all, you'll need to find the RSS feed URL of your blog. It should look something like one of these:

```
http://your-blog.com/rss
http://your-blog.com/feed.xml
```


## **Step 2.** Sign up for Feedburner

You'll need a Feedburner account. Feedburner is one of the tools that google offers, so if you have a primary Google account that you use for other services like Gmail, Google Drive, Google+, or YouTube, then you should set up your Feedburner using that Google account. Or you will need to create a new one.

Sign up for Feedburner using the following link: [Feedburner](http://feedburner.com/)


## **Step 2.** Setup Feedburner

Once logged in Feedburner, it will prompt you to enter your blog's RSS feed URL that you finded before.

![center](/images/adding-email-subscription-button-blog-using-feedburner/1.png)

The next screen will prompt you to enter a title for your feed as well as allow you to customise the feedburner link.

![center](/images/adding-email-subscription-button-blog-using-feedburner/2.png)

The next screen will prompt you to either click "Next" to add additional Feedburner stats to your "feed" or skip ahead to manage your feed. For the purpose of this tutorial, select "Skip directly to feed management" to continue.

![center](/images/adding-email-subscription-button-blog-using-feedburner/3.png)

Once you see the main feed management screen, click on the "Publicize" tab from the top of your screen, choose the "Email Subscriptions" item from left-handed menu of services, and click on the "Activate" button.

![center](/images/adding-email-subscription-button-blog-using-feedburner/4.png)

Feedburner will provide a two kinds of subscribe options. One is a form and the other is just a link. Copy the snippet of link to your clipboard, so you can use it in next step.

![center](/images/adding-email-subscription-button-blog-using-feedburner/5.png)


## **Step 3.** Add an email subscription button to your theme

You can place the snippet of button code anywhere you'd like the email subscription button to display on your theme. 

If your blog based on CMS WordPress, you can use a "Text" widget in the sidebar or footer (if your theme have this option). Jast paste the snippet of button code in the configuration section of widget, save your changes, and that’s it! 

If you’re not using CMS WordPress, you’ll need to find the file of your theme that is responsible for display the default layout of your blog page. Depending on your website platform (WordPress, Joomla, Jekyll, and etc) this file may have the name such as `default.html`, `index.html`, or another name.

**Note:** Your theme may have separate file for display the sidebar or footer. In this case, you'll need a file that may have the name such as `sidebar.html` and `footer.html`, or `sidebar.php` and `footer.php`.


## **Step 4.** Customizing an email subscription button

If you put the original snippet of button code on your blog, it will look like this: <a href="https://feedburner.google.com/fb/a/mailverify?uri=MyCyberUniverse&amp;loc=en_US">Subscribe to My Cyber Universe by Email</a> which opens in a new tab. But you can modify all aspects of the button, and you can style the output the same way you would style any other part of your blog's theme. I show you how to open the link in a pop-up and replace the text with image.

```html
<a href="https://feedburner.google.com/fb/a/mailverify?uri=MyCyberUniverse&amp;loc=en_US" onclick="window.open(this.href, 'popupwindow', 'left=20,top=20,width=540,height=540,scrollbars=yes,toolbar=1,resizable=0'); return false;" class="rss-feed-button">
    <img src="/images/rss-feed.png" />
</a>
<style>
	.rss-feed-button img {
		border: none;
		width: 120px;
		vertical-align: middle;
	}
</style>
```

**Note:** Change the `MyCyberUniverse` to name of your Feedburner feed address.

**Note:** Change the `src` attribute of `img` tag to address of you image.

**Note:** If the images are not showing up on your button, then you may be using relative URL for your images. Use complete URL `http://mycyberuniverse.com/images/rss-feed.png` of the image instead of a relative URL `/images/rss-feed.png`. In Jekyll this can be achieved by using `site.url` or `site.baseurl` variable.

This is how it looks like: <a href="https://feedburner.google.com/fb/a/mailverify?uri=MyCyberUniverse&amp;loc=en_US" onclick="window.open(this.href, 'popupwindow', 'left=20,top=20,width=540,height=540,scrollbars=yes,toolbar=1,resizable=0'); return false;" class="rss-feed-button">
    <img src="/images/adding-email-subscription-button-blog-using-feedburner/rss-feed.png" />
</a>
<style>
	.rss-feed-button img {
		border: none;
		width: 120px;
		vertical-align: middle;
	}
</style>


<br>
That’s it! Now your blog have an email subscription button, so your visitors will be able to subscribe to your blog using their email address, and you will be able to manage and see how many people have subscribed to your blog via Feedburner.


<br>
I hope that helped to setup Feedburner for your blog. Now that you know how it works, subscribe to my blog. Thanks for reading!