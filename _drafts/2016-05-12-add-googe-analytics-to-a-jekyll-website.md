---
lang: en
title: Add Google Analytics to a Jekyll website
date: 2016-05-12T22:35:03+00:00
author: Arthur Gareginyan
layout: post
ref: add-googe-analytics-to-a-jekyll-website
permalink: /web/add-googe-analytics-to-a-jekyll-website.html
categories:
  - web
tags:
  - google analytics
  - analytics
  - jekyll
  - guide

---

![thumb](/images/analytics-logo.png)
Google Analytics allows you to get information about your websites visitors such as the devices or OS they were using and their location. It goes without saying that information like this can be very useful for deciding how best to deliver content.

I have recently added Google Analytics to my Github site that is built using Jekyll, here’s how I did it.

Now, step by step guide.


**1.** Sign up.

First, you need a Google Analytics account. If you have a primary Google account that you use for other services like Gmail, Google Drive, Google+, or YouTube, then you should set up your Google Analytics using that Google account. Or you will need to create a new one.

Sign up for Google Analytics using the following link: [Google Analytics](https://www.google.com/analytics/)


**2.** Create an account for website.

To generate your analytics tracking code you first need to create the account (inside your Google Analytics account) for website. You can do this on the `Admin` tab in your Analytics account.

**Note:** You must to create new one accaut for every website you want to tracking.

![thumb](/images/analytics-logo.png)


**3.** Get the tracking code.

You can find the button called `code` on the bottom of your ad unit.

Once you are finished to create an account for website, you will click the Get Tracking ID button.

Tracking code - is a snippet of JavaScript that collects and sends data to Analytics from a website. It’s automatically generated for every web property.

Your tracking code (in this example is Universal Analytics) will be similar to the following one:

```
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


**4.** Create the template with your tracking code.

Create a file called `google-analytics.html` in the `_includes` catalog of your Jekyll website. Insert your tracking code to this file.

Copy this code and I recommend that you paste it within the `_layouts/default.html` file, right towards the top within the `<head>` tag. This will ensure that the code snippet will be added to every page so you can keep track of your whole website.

add the tracking code before the </head> tag on 


**5.** Call the advertisements template in a post template.

Go into the `_layouts` catalog and find the `post.html` file (or any layout file for which you would like ads displayed) and insert the following code.

```
{% raw %}{% include google-analytics.html %}{% endraw %}
```

I place this right after the `{{ content }}`, but the placements is totally up to you. In my case an ads will be displayed at the end of each blog post, just above the comments section.


**6.** Reporting.

Now you are all set up, simply publish your website (note your website must be live for this to take effect). Then within the Google Analytics home page, select the `Reporting` tab at the top of the page. From here you will be able to see reports for the number of page views, geospatial information, technology and even your sites behaviour.
