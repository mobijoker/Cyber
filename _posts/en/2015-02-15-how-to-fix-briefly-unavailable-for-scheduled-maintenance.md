---
id: 540
lang: en
ref: how-to-fix-briefly-unavailable-for-scheduled-maintenance
title: 'How to fix: “Briefly unavailable for scheduled maintenance”'
date: 2015-02-15T13:36:33+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=540
permalink: /web/how-to-fix-briefly-unavailable-for-scheduled-maintenance.html
switch_like_status:
  - 1
categories:
  - Error
  - Web
tags:
  - cms wordpress
  - error
  - how to fix
  - maintenance
  - wordpress

---

![thumb](/images/error.png)
How to, in the CMS WordPress, fix the error due to which is displayed the message "Briefly unavailable for scheduled maintenance. Check back in a minute."


### What causes this problem

Maintenance mode page is technically not an error. It is a notification page.

When WordPress is automatically updating the core WordPress files, plugins or themes, your site is marked as under maintenance mode by creating a file named .maintenance in the root directory (directory that contains the `wp-admin`). If that file exists, then vistors will see the message: “**Briefly unavailable for scheduled maintenance. Check back in a minute.**”.

If everything worked normally, then this notice will be displayed for only a few seconds. However, sometimes due to a web server’s slow response or low memory issue, the update script may timeout or gets interrupted. When this happens, WordPress does can't deduce your site from the maintenance mode. Unless this file is removed your site will remain in the maintenance mode and visitors of your website will continue to see the notification.


### How to fix it

Fortunately the fix is fairly simple, you need to attach to your site using ftp, ssh or with the file manager in your hosting account and in the root directory (directory that contains the `wp-admin`) you will see a file called `.maintenance`, simply delete this file and your site will come back to life.

**NOTE:** This file are marked as hidden, so you may need to enable show hidden files on your FTP client before you can see it. For example, on Filezilla, you can force it to show hidden files by clicking on `Server` -&gt; `Force showing hidden files` from the menu bar.

An unfinished or interrupted update may cause issues when your site comes out of maintenance mode. So, once you have deleted the .maintenance file, it is a good idea to re-apply the updates you were doing to make sure they have been completed correctly.
