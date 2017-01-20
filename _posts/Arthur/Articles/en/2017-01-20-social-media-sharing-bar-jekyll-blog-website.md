---
title: Social Media Share Bar for Jekyll blog/website
ref: social-media-share-bar-jekyll-blog-website
permalink: /web/social-media-share-bar-jekyll-blog-website.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - share
  - sharing
  - share bar
  - sharing bar
  - share button
  - sharing button
  - MyCyberUniverse share bar
  - MyCyberUniverse sharing bar
  - social media
  - socila media sharing
  - social media share bar
  - social media buttons
  - social media widget
  - post sharing
  - page sharing
  - article sharing
  - how to
  - tutorial
  - jekyll
  - jekyll widget
  - jekyll plug-in

---

![thumb](/images/articles/social-media-share-bar-jekyll-blog-website/thumbnail.png)
Allowing users to share your articles on social media is a common blog/website feature. More share is equal to more eyeballs on your article. Shares will drive traffic to your blog/website and sometimes it may go viral. But, if you read a lot over the internet then you know how hard it is to share an interesting article with your friends if it doesn’t have a share buttons, so it is necessary to provide an option to share. In this article I show you how I added the social media share bar widget to this Jekyll website.

Adding a share bar to website is a really easy process when using special free services, but I'm a programmer and designer, so I had created the share bar by myself. To make it the Jekyll way, I did the share bar in a widget format. I call it a widget, since it can be reused.

Here's how it looks like:
![center](/images/articles/social-media-share-bar-jekyll-blog-website/preview.png)

Currently, I’m using this social media share bar widget on my website, so you'll see it at the end of this article.

Now, step by step guide.


## **Step 1.** Create a widget

First of all, you’ll need to create a new HTML file inside the `_includes` catalog and call it `share-bar.html`. Then place the following code to this file:

```html
{% raw %}
<br>
<div id="share-bar">

	<h4>Share this:</h4>

	<div class="share-buttons">
	    <a  href="https://www.facebook.com/sharer/sharer.php?u={{ site.url }}{{ site.baseurl }}{{ page.url }}"
	        onclick="window.open(this.href, 'pop-up', 'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;"
	        title="Share on Facebook" >
	        <i class="fa fa-facebook-official share-button"> facebook</i>
	    </a>

	    <a  href="https://twitter.com/intent/tweet?text={{ page.title }}&url={{ site.url }}{{ site.baseurl }}{{ page.url }}"
	        onclick="window.open(this.href, 'pop-up', 'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;"
	        title="Share on Twitter" >
	        <i class="fa fa-twitter share-button"> twitter</i>
	    </a>

	    <a  href="https://plus.google.com/share?url={{ site.url }}{{ site.baseurl }}{{ page.url }}"
	        onclick="window.open(this.href, 'pop-up', 'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;"
	        title="Share on Google+" >
	        <i class="fa fa-google-plus share-button"> google</i>
	    </a>

	    <a  href="http://pinterest.com/pin/create/button/?url={{ site.url }}{{ site.baseurl }}{{ page.url }}"
	        onclick="window.open(this.href, 'pop-up', 'left=20,top=20,width=900,height=500,toolbar=1,resizable=0'); return false;"
	        title="Share on Pinterest" >
	        <i class="fa fa-pinterest-p share-button"> pinterest</i>
	    </a>

	    <a  href="http://www.tumblr.com/share/link?url={{ site.url }}{{ site.baseurl }}{{ page.url }}"
	        onclick="window.open(this.href, 'pop-up', 'left=20,top=20,width=900,height=500,toolbar=1,resizable=0'); return false;"
	        title="Share on Tumblr" >
	        <i class="fa fa-tumblr share-button"> tumblr</i>
	    </a>

	    <a  href="http://www.reddit.com/submit?url={{ site.url }}{{ site.baseurl }}{{ page.url }}"
	        onclick="window.open(this.href, 'pop-up', 'left=20,top=20,width=900,height=500,toolbar=1,resizable=0'); return false;"
	        title="Share on Reddit" >
	        <i class="fa fa-reddit-alien share-button"> reddit</i>
	    </a>

	    <a  href="https://www.linkedin.com/shareArticle?mini=true&url={{ site.url }}{{ site.baseurl }}{{ page.url }}&title={{ page.title }}&summary={{ page.description }}&source=webjeda"
	        onclick="window.open(this.href, 'pop-up', 'left=20,top=20,width=500,height=500,toolbar=1,resizable=0'); return false;"
	        title="Share on LinkedIn" >
	        <i class="fa fa-linkedin share-button"> linkedin</i>
	    </a>

	    <a  href="mailto:?subject={{ page.title }}&amp;body=Check out this site {{ site.url }}{{ site.baseurl }}{{ page.url }}"
	        title="Share via Email" >
	        <i class="fa fa-envelope share-button"> email</i>
	    </a>
	</div>

</div>
{% endraw %}
```

> **Note:** The links are built using liquid code. They look for current page URL and insert it into the share link. So doesn’t matter where you place them, they will work.



## **Step 2.** Add the Font-Awesome iconic font

In the social media share bar I have used an icons of social media and email from the Font-Awesome iconic font which is better than loading an image files localy or remotely. If your theme already have the buil-in Font-Awesome library then just go to next step of this tutorial. 

If your theme doesn't have a Font-Awesome library icluded then add the following code to the head section (right before the `</head>` tag) of your theme (it maybe a `head.html` file in the `_includes` catalog), or add it to the begining of the `share-bar.html` file that you maked in the first step of this tutorial:

```html
<link href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet">
```

> **Note:** A good way to avoid the Font-Awesome library loading delay is to optimize the Font-Awesome library by removing all you not needed icons from it.



## **Step 3.** Styling for the widget

You can style your share bar the same way you would style any other part of your blog/website theme. Use a style that suits your needs. I have styled the share bar with the following CSS code:

```css
/* Share Bar */
#share-bar {
    font-size: 20px;
}

/* Title */
#share-bar h4 {
    margin-bottom: 10px;
    font-weight: 500;
}

/* All buttons */
.share-buttons {
}
 
/* Each button */
.share-button {
    margin: 0px;
    margin-bottom: 10px;
    margin-right: 3px;
    border: 1px solid #D3D6D2;
    padding: 5px 10px 5px 10px;
}
.share-button:hover {
    opacity: 1;
    color: #ffffff;
}

/* Facebook button */
.fa-facebook-official {
    color: #3b5998;
}
.fa-facebook-official:hover {
    background-color: #3b5998;
}

/* Twitter button */
.fa-twitter {
    color: #55acee;
}
.fa-twitter:hover {
    background-color: #55acee;
}

/* Google-PLus button */
.fa-google-plus {
    color: #dd4b39;
}
.fa-google-plus:hover {
    background-color: #dd4b39;
}

/* Pinterest button */
.fa-pinterest-p {
    color: #cb2027;
}
.fa-pinterest-p:hover {
    background-color: #cb2027;
}

/* Tumblr button */
.fa-tumblr {
    color: #32506d;
}
.fa-tumblr:hover {
    background-color: #32506d;
}

/* Reddit button */
.fa-reddit-alien {
    color: #ff4500;
}
.fa-reddit-alien:hover {
    background-color: #ff4500;
}

/* LinkedIn button */
.fa-linkedin {
    color: #007bb5;
}
.fa-linkedin:hover {
    background-color: #007bb5;
}

/* Email button */
.fa-envelope {
    color: #444444;
}
.fa-envelope:hover {
    background-color: #444444;
}
```

> **Note:** You can add this CSS code to your Jekyll theme stylesheet file (it maybe a `_layout.scss` file in the `_sass` catalog) or just add it to the end of the `share-bar.html` file that you maked in the first step of this tutorial, but don't forget to wrap it with the `<style></style>` tag.

> **Note:** I have used only the official colors for the social media icons.



## **Step 4.** Add to the theme

Now you have to hook up the share bar widget anywhere in your theme where you’d like to display the share bar. To display it at the end of each post just copy the following short code to your post layout file which will be inside the `_layouts` catalog and are named `post.html`.

```
{% raw %}{% include  share-bar.html %}{% endraw %}
```

> **Note:** This short code is just includes the contents of the `share-bar.html` file into this place.

> **Note:** You can add this short code in any place of your theme: inside the post content, in the sidebar area, in the footer area and etc..

In my website theme I added this short code right after the `{% raw %}{{ content }}{% endraw %}` line. Here is a snippet from my `post.html` file:

```html
{% raw %}<div class="post-content" itemprop="articleBody">
	{{ content }}
	{% include  share-bar.html %}
</div>{% endraw %}
```



## **Step 5.** Add the Open Graph, Twitter Card Tags and Schema.org microdata

Finally, you may want to add some Open Graph, Twitter Card Tags and Schema.org microdata to your blog pages, this will create that pretty share dialog and turn on the share tracking/analytics. You can test/validate this microdata [here](https://developers.facebook.com/tools/debug/sharing) and [here](https://cards-dev.twitter.com/validator). Read about the Open Graph you can [here](http://ogp.me/), about the Twitter Card Tags [here](https://dev.twitter.com/cards/markup) and about the Schema.org microdata [here](https://developers.google.com/+/web/snippet/).

And you’re done! 


## Summarizing

Now your blog/website will have the social media share bar at the end of each post, so visitors of your blog/website will be able to share any article that they liked on social media.

This way I have added the social media share bar to my website. This is one of the reasons I love Jekyll, all things can be done simply by creating a small widget. So simple isn’t it?

Now when you know how it works, share this article. Why not give these buttons a try before implementing on your blog/website? :)

If you were able to implement this on your blog/website then please leave a link in the comment.

Thanks for reading!