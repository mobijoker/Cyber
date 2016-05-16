---
title: Add Googe AdSense to a Jekyll website
ref: add-googe-adsense-to-a-jekyll-website
permalink: /web/add-googe-adsense-to-a-jekyll-website.html
date: 2016-05-12T22:35:03+00:00
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - monetize
  - adsense
  - google adsense
  - revenue
  - ad
  - advertisement
  - money
  - jekyll
  - guide

---

![thumb](/images/adsense-logo.png)
Google AdSense is a free, simple way to earn money by placing third-party advertisements on a website. My Github hosted Jekyll website is being used primarily as a blog as you can see, so I wanted to host an advertisement at the end of each blog post, just above the comments section.

Now, step by step guide.

**1.** Sign up.

First, you need a Google AdSense account. If you have a primary Google account that you use for other services like Gmail, Google Drive, Google+, or YouTube, then you should set up your Google AdSense using that Google account. Or you will need to create a new one.

Sign up for Google AdSense using the following link: [Google AdSense](https://www.google.com/adsense/)


**2.** Create the ad unit.

To generate your AdSense ad code you first need to create the ad unit. You can do this on the `My ads` tab in your AdSense account.

Ad unit - is set of Google ads displayed as a result of one piece of AdSense ad code. There are a few different types of ad unit that you can choose from.


**3.** Get the ad code.

You can find the button called `code` on the bottom of your ad unit.

![](/images/adsense-code.png)

Your ad code will be similar to the following one:

```
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<!-- Single post - 1 (yourwebsite.com) -->
<ins class="adsbygoogle"
    style="display:block"
    data-ad-client="0000000000000000"
    data-ad-slot="00000000"
    data-ad-format="auto"></ins>
<script>
    (adsbygoogle = window.adsbygoogle || []).push({});
</script>
```

**Note:** This is sample code only, please don't use it on your own website.


**4.** Create the template with your ad code.

Create a file called `advertisements.html` in the `_includes` catalog of your Jekyll website. Insert your ad code to this file.


**5.** Call the advertisements template in a post template.

Go into the `_layouts` catalog and find the `post.html` file (or any layout file for which you would like ads displayed) and insert the following code.

```
{% raw %}{% include advertisements.html %}{% endraw %}
```

I place this right after the `{{ content }}`, but the placements is totally up to you. In my case an ads will be displayed at the end of each blog post, just above the comments section.

You just need to wait a few days and then you should recieve an ads on all pages that utilise that layout.

Each month, you can have the money deposited directly into your bank account or mailed to you as a check. By the way, Google only mails you a check after you accumulate $100 worth of revenue.

**Note:** To see the ads by Google AdSense running on your website, remember to temporary disable your adblocker.
