---
title: Adding an email subscription form to your blog by using Feedburner
ref: adding-email-subscription-form-blog-using-feedburner
permalink: /web/adding-email-subscription-form-blog-using-feedburner.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - feedburner
  - subscription form
  - subscription
  - subscribe
  - email subscription

---

![thumb](/images/adding-email-subscription-form-blog-using-feedburner/sign-up.png)
A great way to keep up to date with a blog that you love to follow is to subscribe to an email subscription of their posts. That way, when a new post is made, it lands right in your email inbox. If you want to offer this to people who visit your blog, it is easy to do. In this article I show you how to add to your blog an email subscription form that connected to Feedburner.

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


## **Step 3.** Setup Feedburner

Once logged in Feedburner, it will prompt you to enter your blog's RSS feed URL that you finded before.

![center](/images/adding-email-subscription-form-blog-using-feedburner/1.png)

The next screen will prompt you to enter a title for your feed as well as allow you to customise the feedburner link.

![center](/images/adding-email-subscription-form-blog-using-feedburner/2.png)

The next screen will prompt you to either click "Next" to add additional Feedburner stats to your "feed" or skip ahead to manage your feed. For the purpose of this tutorial, select "Skip directly to feed management" to continue.

![center](/images/adding-email-subscription-form-blog-using-feedburner/3.png)

Once you see the main feed management screen, click on the "Publicize" tab from the top of your screen, choose the "Email Subscriptions" item from left-handed menu of services, and click on the "Activate" button.

![center](/images/adding-email-subscription-form-blog-using-feedburner/4.png)

Feedburner will provide a two kinds of subscribe options. One is a form and the other is just a link. Copy the snippet of form code to your clipboard, so you can use it in next step.

![center](/images/adding-email-subscription-form-blog-using-feedburner/5.png)


## **Step 4.** Add an email subscription form to your theme

You can place the snippet of form code anywhere you'd like the email subscription form to display on your theme. 

If your blog based on CMS WordPress, you can use a "Text" widget in the sidebar or footer (if your theme have this option). Jast paste the snippet of form code in the configuration section of widget, save your changes, and that’s it! 

If you’re not using CMS WordPress, you’ll need to find the file of your theme that is responsible for display the default layout of your blog page. Depending on your website platform (WordPress, Joomla, Jekyll, and etc) this file may have the name such as `default.html`, `index.html`, or another name.

**Note:** Your theme may have separate file for display the sidebar or footer. In this case, you'll need a file that may have the name such as `sidebar.html` and `footer.html`, or `sidebar.php` and `footer.php`.

**Note:** You can modify all aspects of the form, and you can style the output the same way you would style any other part of your blog's theme.


<br>
That’s it! Now your blog have an email subscription form, so your visitors will be able to subscribe to your blog using their email address, and you will be able to manage and see how many people have subscribed to your blog via Feedburner.


## Email Subscription Form on my Blog

For display an email subscription form on my Jekyll blog I chooses a footer section. I modified the snippet of form code and added some style sheet. Here's what I got:

```html
<div class="widget-subscribe">
    <h6 class="widget-footer-title">Subscribe</h6>
    <p>Subscribe to our Newsletter and get new posts delivered to your inbox - free!</p>
    <form action="https://feedburner.google.com/fb/a/mailverify" method="post" target="popupwindow" onsubmit="window.open('https://feedburner.google.com/fb/a/mailverify?uri=MyCyberUniverse', 'popupwindow', 'scrollbars=yes,width=550,height=520');return true">
        <input type="email" name="email" placeholder="Email address" class="subscribe-input">
        <input type="hidden" value="MyCyberUniverse" name="uri"/>
        <input type="hidden" name="loc" value="en_US"/>
        <button type="submit" value="Subscribe" name="subscribe" class="subscribe-button">Subscribe</button>
    </form>
</div>
```

```css
<style>
.widget-subscribe {
    float: right;
    width: 100%;
    padding-bottom: 30px;
}
.widget-footer-title {
    color: #fff;
    text-transform: uppercase;
    font-size: 14px;
    margin-bottom: 15px;
    font-weight: 700;
}
.subscribe-form {
    position: relative;
    margin-top: 10px;
}
.subscribe-input {
    
    box-sizing: border-box;
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
    border-radius: 4px;
    -moz-border-radius: 4px;
    -webkit-border-radius: 4px;
    background-color: #fff;
    width: -webkit-calc(100% - 130px );
    width: calc(100% - 130px );
    padding: 10px 40px 10px 10px;
    color: #999;
    font-size: 14px;
    line-height: normal;
}
.subscribe-button {
    position: relative;
    display: inline-block;
    top: -3px;
    font-family: Trajan Pro;
    font: 500 15px/15px 'Trajan Pro';
    text-transform: uppercase;
    text-align: center;
    vertical-align: middle;
    color: #fff;
    cursor: pointer;
    background: #19b4cf;
    padding: 14px 15px 10px 12px;
    border: 0;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    border-radius: 3px;
    -webkit-box-shadow: 0px 3px 0px 0px #148ea4;
    -moz-box-shadow: 0px 3px 0px 0px #148ea4;
    box-shadow: 0px 3px 0px 0px #148ea4;
    -webkit-transition: color 0.3s, background 0.3s, box-shadow 0.3s, border-color 0.3s;
    -moz-transition: color 0.3s, background 0.3s, box-shadow 0.3s, border-color 0.3s;
    transition: color 0.3s, background 0.3s, box-shadow 0.3s, border-color 0.3s;
}
.subscribe-button:hover {
    background: #0093b1;
    -webkit-box-shadow: 0px 3px 0px 0px #0F7183;
    -moz-box-shadow: 0px 3px 0px 0px #0F7183;
    box-shadow: 0px 3px 0px 0px #0F7183;
}
</style>
```

You can use this on your own blog, but do not forget to change the `MyCyberUniverse` to name of your Feedburner feed address.

<br>
I hope that helped to setup Feedburner for your blog. Now that you know how it works, subscribe to my blog. Thanks for reading!