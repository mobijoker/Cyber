---
title: "How to fix: MailChimp Subscriber Pop-Up not working in WordPress"
ref: mailchimp-subscriber-popup-not-working-in-wordpress
permalink: /mailchimp-subscriber-popup-not-working-in-wordpress.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - error
  - web
tags:
  - wordpress
  - wordpress mailchimp
  - wordpress and mailchimp
  - mailchimp
  - mailchimp subscription
  - subscription popup
  - subscription
  - subscription form
  - subscribe
  - subscriber form
  - error
  - subscriber popup
  - mailchimp popup
  - mailchimp subscriber popup

---

![thumb](/images/articles/mailchimp-subscriber-popup-not-working-in-wordpress/mailchimp.png)
MailChimp is a great solution to add the subscription form to our websites. The only problem is that the MailChimp Subscriber Pop-Up doesn’t work on WordPress websites. I added the MailChimp Subscriber Pop-Up embed code to one of my WordPress websites, but nothing happened when I loaded any website page where the pop-up should have appeared. I searched Google and noticed that many others have the same issue in WordPress.

Example of the MailChimp Subscriber Pop-Up embed code:

```
<script type="text/javascript" src="//s3.amazonaws.com/downloads.mailchimp.com/js/signup-forms/popup/embed.js" data-dojo-config="usePlainJson: true, isDebug: false"></script>
<script type="text/javascript">require(["mojo/signup-forms/Loader"], function(L) { L.start({"baseUrl":"mc.us14.list-manage.com","uuid":"xxxxxxxxxxxxxxxxxxxxxxxxxx","lid":"xxxxxxxxxxx"}) })</script>
```


### What causes this problem

By analyzing the output code of the page I noticed that the MailChimp Subscriber Pop-up embed code (file at `//s3.amazonaws.com/downloads.mailchimp.com/js/signup-forms/popup/embed.js`) tries to load the `jquery.js` file from the root directory of the website. But in WordPress, the [jquery.js](https://jquery.com/) file located in the `/wp-includes/js/jquery/` directory.


### How to fix it

In order to get it work we need to add the `jquery.js` file to the root directory of the website. We will create file with the `jquery.js` name, but the content will be loaded from the `jquery.js` file that supplied with WordPress. Now, step by step.

**Step 1.** [Design your MailChimp Subscriber Pop-up](http://kb.mailchimp.com/lists/signup-forms/add-a-pop-up-signup-form-to-your-website) and copy the MailChimp Subscriber Pop-up embed code that will be offered to you.

![](/images/articles/mailchimp-subscriber-popup-not-working-in-wordpress/1.png)

**Step 2.** In WordPress Admin Panel install and activate the [Head and Footer Scripts Inserter](https://wordpress.org/plugins/header-and-footer-scripts-inserter/) plugin.

![](/images/articles/mailchimp-subscriber-popup-not-working-in-wordpress/2.png)

**Step 3.** In WordPress Admin Panel go to plugin settings page (`Settings -> Head and Footer Scripts Inserter`). Paste the code (that you got on step 2) to the bottom field of this page, and click on the `Save Changes` button.
 
![](/images/articles/mailchimp-subscriber-popup-not-working-in-wordpress/3.png)

**Step 4.** Create an empty text file with the name `jquery.js`. Open it in the text editor and paste the following code into it:

```
jQuery.getScript("/wp-includes/js/jquery/jquery.js").done(function(){ })
```

**Step 5.** Using FTP or your cPanel File Manager move the `jquery.js` file (that you created on step 4) to the root directory of your website. Usually the root directory is a directory with name `www` if you use cPanel, or `httpdocs` if you use Parallels Plesk Panel.


Done! Now, when you load any page on your website, your MailChimp subscribe pop-up should work.

> **Note:** The MailChimp stores a cookie for one year to prevent you from seeing a pop-up repeatedly after you've closed it or filled it in. Don’t fall into the trap of thinking that the pop-up doesn’t work when it actually does. If you're testing this you may need to clear cookies, use a different browser, or open a private browser window to see the form on repeat visits after dismissing or filling it.
