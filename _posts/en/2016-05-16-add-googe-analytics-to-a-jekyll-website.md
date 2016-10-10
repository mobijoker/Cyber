---
title: Add Google Analytics to a Jekyll website
ref: add-googe-analytics-to-a-jekyll-website
permalink: /web/add-googe-analytics-to-a-jekyll-website.html
date: 2016-05-16
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - google analytics
  - analytics
  - jekyll
  - guide

---

![thumb](/images/add-googe-analytics-to-a-jekyll-website/analytics-logo.png)
Google Analytics allows you to get information about your websites visitors such as the devices or OS they were using and their location. Such information can be very useful for deciding how best to deliver content. Below, I’ll explain how to set up a Google Analytics on Github website that is built using Jekyll.

<br><br>

Now, step by step guide.

**Step 1.** Sign up.

First, you need a Google Analytics account. If you have a primary Google account that you use for other services like Gmail, Google Drive, Google+, or YouTube, then you should set up your Google Analytics using that Google account. Or you will need to create a new one.

Sign up for Google Analytics using the following link: [Google Analytics](https://www.google.com/analytics/)


**Step 2.** Create an account for website.

To generate your analytics tracking code you first need to create the account (inside your Google Analytics account) for website. You can do this on the `Admin` tab in your Analytics account.

**Note:** You must to create new one accaut for every website you want to tracking.

![](/images/add-googe-analytics-to-a-jekyll-website/analytics-account.png)


**Step 3.** Get the tracking code.

Tracking code - is a snippet of JavaScript that collects and sends data to Analytics from a website. It’s automatically generated for every web property.

Once you are finished to create an account for website, you will click the "Get Tracking ID" button. Your tracking code (in this example is Universal Analytics) will be similar to the following one:

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

**Note:** This is sample code only, please don't use it on your own website.


**Step 4.** Create the template with your tracking code.

Create a file called `google-analytics.html` in the `_includes` catalog of your Jekyll website. Insert your tracking code to this file.


**Step 5.** Call the google-analytics template from a default template.

Go into the `_layouts` catalog, find the `default.html` file and insert the following code right before the `</head>` tag.

```
{% raw %}{% include google-analytics.html %}{% endraw %}
```

This will ensure that the code snippet will be added to every page so you can keep track of your whole website.

**Note:** Some themes have a separeted file with head section (`<head></head>` tags). This file can be named `head.html` and be placed in the `_includes` catalog.


That’s it! Once tracking is set up, Google Analytics will start collecting data immediately. After a few days, you can start reviewing the reports.
