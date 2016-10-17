---
title: Add icon-fonts to Adobe Muse website
ref: add-icon-fonts-adobe-muse-website
permalink: /web/add-icon-fonts-adobe-muse-website.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - Web
tags:
  - fontawesome
  - font awesome
  - google icons
  - bootstrap icons
  - adobe muse
  - iconfont
  - icon-font
  - icon font
  - web font
  - font

---

![thumb](/images/add-icon-fonts-adobe-muse-website/cloud.png)
The beauty of icon-fonts is that they are in essence, fonts. Which means they can be used much like any other piece of text. Unlike images they can have their colour changed easily, can be scaled and are lightweight in download terms. And they are fully responsive and retina friendly. The huge choice available at Font Awesome, Bootstrap and Google font icons means that you should find the exact graphic you are looking for and when combined with other muse assets you can quickly and easily build buttons, graphics and widgets. In this article you’ll learn how to use and customize the Font Awesome, Bootstrap and Google font icons in any Muse website.

<br><br>

Open Adobe Muse as you normally would and do the following.


## **Step 1.** Adding the icon-fonts to Adobe Muse project

First, you need to add the icon-fonts to your Muse project so that you could use the icons. This can be done simple by adding one line of code into your website’s Master Page Properties `metadata` section. This line is a HTML link to CSS stylesheet hosted on a CDN (Content Distribution Network). It's great as it means you do not need to upload any files to a server as the icon-fonts are being pulled directly from internet. The downside is that you do need to be working online if you want to preview the icons whilst working with them. Also note that Muse may slow down while working with icon-fonts due to re-rendering each time you adjust the fonts.

**a)** Navigate to the `Plan View` and double click the `A-Masters` thumbnail in the `Masters` section.

**b)** Click `Page` → `Page Properties`.

**c)** Go to the `Meta Data` tab in the panel and paste on of the following line (you can add all three icon-fonts) into the `HTML for <head>` area of the panel. 

![](/images/add-icon-fonts-adobe-muse-website/icon-fonts-1.png)

Font Awesome icon-font:

```html
<link rel="stylesheet" href="http://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.4.0/css/font-awesome.min.css">
```

Bootstrap icon-font:

```html
<link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/bootstrap/3.3.4/css/bootstrap.min.css">
```
Google icon-font:

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/icon?family=Material+Icons">
```

**Note:** This will add the code to all subsequent pages you build in Muse using that `Master`. But you may want to add the icon-fonts only to a specific page, for this you need to open `Page Properties` of a specific page.

Close the panel and thats it. You can now start adding icons to the page.


## **Step 2.** Adding an icon to a page

**a)** Navigate to Font Awesome, Bootstrap or Google icons page and choose the one you like. Copy the code for this icon. For example, for the cloud icon the code will be as follows:

Font Awesome icon:

```html
<i class="fa fa-cloud"></i>
```

Bootstrap icon:

```html
<i class="glyphicon glyphicon-cloud"></i>
```

Google icon:

```html
<i class="material-icons">cloud</i>
```

**b)** Open any page of your Muse project from the `Plan View`.

**c)** Simply right click and paste (or Command-V for Mac, Ctrl-V for Windows) the code anywhere on the page. After a second or two, while Muse makes the connection to the CDN, the icon will appear on the page. You should now have something that looks like this:

![](/images/add-icon-fonts-adobe-muse-website/icon-fonts-2.png)


## **Step 3.** Stylize an icon

Now you can make your icon look a bit better using the text controls menu. From this menu you can change the size and color of icon, also icon can be centered and much more.

**a)** Select the icon you have just placed on the page.

**b)** Go to the text controls menu.

**c)** Here change what you like.

![](/images/add-icon-fonts-adobe-muse-website/icon-fonts-3.png)

**Note:** There will be a slight pause as Muse renders the font. Notice how the font has resized and has kept its quality as it is a vector font.
