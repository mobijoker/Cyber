---
id: 506
lang: en
ref: horizontal-navigation-menu-in-blogger
title: Horizontal Navigation Menu in Blogger
date: 2015-01-31T00:09:08+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=506
permalink: /web/horizontal-navigation-menu-in-blogger.html
categories:
  - Web
tags:
  - blogger
  - menu
  - navigation

---

![thumb](/images/blogger-logo.png)
Navigation menu is an essential part of any blog or website. It helps visitors to easily get the required content the whole blog.
I'll show how to add the horizontal navigation double menu. In the left part which is Pages and in the right part is Labels (Category).


So let’s get started add navigation menu in blogger.

**Step 1.** Login to Blogger account and go to Blogger Dashboard.

**Step 2.** Go to the “Layout” tab by clicking on the “Layout” text in the left pane.

**Step 3.** Click on the “Add a Gadget link” (In The Header Area). In the pop-up box with the list of gadgets choose “Pages” by clicking the blue plus sign for that gadget. Configure “Pages” gadget and click on the “Save” button.

**Step 4.** Click on “Add a Gadget link” (In The Header Area). In the pop-up box with the list of gadgets choose “Labels” by clicking the blue plus sign for that gadget. Configure “Labels” gadget and click on “Save” button.

**Step 5.** Move gadgets "Pages" and "Labels" side by side below the title of the blog.

**Step 6.** Go to the “Template” tab by clicking on the “Template” text in the left pane.

**Step 7.** Click on the "Customize" button to go to the section "Blogger Template Designer".

**Step 8.** Click on “Advanced” then click on “Add CSS”, add the code given below to field “Add custom CSS” and click on '”Apply to Blog” button.

```
/* NAVIGATION MENU
***************************/
.fauxborder-left .tabs-fauxborder-left {
padding-top: 5px;
border-top: 1px solid #cccccc;
border-bottom: 1px solid #cccccc;
height: 40px;
}
#Label1 {
margin-top: 0;
}
.tabs-inner .section:first-child {
border: 0;
}
#crosscol {
display: block;
position: absolute;
left: 10%
}
#crosscol-overflow {
display: block;
position: absolute;
right: 10%
}
#crosscol-overflow .widget ul{
overflow: hidden;
display: inline-block;
border-radius: 4px;
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
box-shadow: 0 0 4px rgba(255, 255, 255, 0.6);
-moz-box-shadow: 0 0 4px rgba(255, 255, 255, 0.6);
-webkit-box-shadow: 0 0 4px rgba(255, 255, 255, 0.6);
}
#crosscol-overflow .widget ul li{
background-color: #f0f0f0;
background-image: -webkit-gradient(linear,left top, left bottom,from(#fefefe), color-stop(0.5,#f0f0f0), color-stop(0.51, #e6e6e6));
background-image: -moz-linear-gradient(#fefefe 0%, #f0f0f0 50%, #e6e6e6 51%);
background-image: -o-linear-gradient(#fefefe 0%, #f0f0f0 50%, #e6e6e6 51%);
background-image: -ms-linear-gradient(#fefefe 0%, #f0f0f0 50%, #e6e6e6 51%);
background-image: linear-gradient(#fefefe 0%, #f0f0f0 50%, #e6e6e6 51%);
border-right: 1px solid rgba(9, 9, 9, 0.125);
box-shadow: 1px -1px 0 rgba(255, 255, 255, 0.6) inset;
-moz-box-shadow: 1px -1px 0 rgba(255, 255, 255, 0.6) inset;
-webkit-box-shadow: 1px -1px 0 rgba(255, 255, 255, 0.6) inset;
position:relative;
float: left;
list-style: none;
line-height: 258%;
}
```

**Step 9.** Now add labels to all post's in the `Posts` tab -&gt; `Edit` -&gt; `Post Settings` -&gt; `Labels` and you done.

**NOTE:** This solution for "Simple" template.
