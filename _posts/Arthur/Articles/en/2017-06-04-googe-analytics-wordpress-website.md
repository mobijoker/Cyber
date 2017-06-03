---
title: Add Google Analytics to WordPress website
ref: googe-analytics-wordpress-website
permalink: /web/googe-analytics-wordpress-website.html
date: 2017-06-04
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - google analytics
  - universal analytics
  - google tracking code
  - analytics tracking code
  - analytics
  - wordpress
  - wp
  - guide
  - manual
  - step by step

---

![thumb](/images/articles/googe-analytics-wordpress-website/thumbnail.png)
Google Analytics allows you to get information about your websites visitors such as the devices or OS they were using and their location. Such information can be very useful for deciding how best to deliver content. Below, I’ll explain how to set up a Google Analytics on the WordPress website.

<br>

Now, step by step guide.


## **Step 1.** Sign up

First of all, you need a Google Analytics account. If you have a primary Google account that you use for other services like Gmail, Google Drive, Google+, or YouTube, then you should set up your Google Analytics using that Google account. Or you will need to create a new one.

Sign up for Google Analytics using the following link: [Google Analytics](https://www.google.com/analytics/)


## **Step 2.** Create an account for website

To generate your analytics tracking code you first need to create the account (inside your Google Analytics account) for website. You can do this on the `Admin` tab in your Analytics account.

> **Note:** You must to create new one accaut for every website you want to tracking.

![](/images/articles/googe-analytics-wordpress-website/image-1.png)


## **Step 3.** Get the tracking code

Tracking code - is a snippet of JavaScript that collects and sends data to Analytics from a website. It’s automatically generated for every web property.

Once you are finished to create an account for website, you will click the `Get Tracking ID` button.

![](/images/articles/googe-analytics-wordpress-website/image-2.png)

Your tracking code (in this example is Universal Analytics) will be similar to the following one:

```js
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  ga('create', 'XXXXXXXXXXXX', 'auto');
  ga('send', 'pageview');

</script>
```

> **Note:** This is sample code only, please don't use it on your own website.


## **Step 4.** Install plugin for adding a tracking code

Next, let’s install the [Head and Footer Scripts Inserter](https://wordpress.org/plugins/header-and-footer-scripts-inserter/) plugin, through which we will add the Google Analytics tracking code to our website. You can install it just as you would any other WordPress Plugin. Here are two methods (automatic and manual):

Automatically via WordPress Admin Panel:

1. Log into Admin Panel of your WordPress website.
2. Go to `Plugins` &#8680; `Add New`.
3. Find this plugin and click install.
4. Activate this plugin through the `Plugins` tab.

Manually via FTP access:

1. Download a copy (ZIP file) of this plugin from [WordPress.org](https://wordpress.org/plugins/header-and-footer-scripts-inserter/).
2. Unzip the ZIP file.
3. Upload the unzipped catalog to your website's plugin directory (`/wp-content/plugins/`).
4. Log into Admin Panel of your WordPress website.
5. Activate this plugin through the `Plugins` tab.

After installation, a `Head and Footer Scripts Inserter` menu item will appear in the `Settings` section. Click on this in order to view plugin administration page.

![](/images/articles/googe-analytics-wordpress-website/image-3.png)


## **Step 5.** Add the Google Analytics tracking code to plugin

Go to the "Head and Footer Scripts Inserter" plugin administration page and insert your tracking code to the first top field. This will ensure that the code snippet will be added to every page so you can keep track of your whole website.

![](/images/articles/googe-analytics-wordpress-website/image-4.png)

That’s it! Once tracking is set up, Google Analytics will start collecting data immediately. After a few days, you can start reviewing the reports.
