---
title: Integrate Flatr button to Jekyll website
ref: integrate-flattr-button-jekyll-website
permalink: /web/integrate-flattr-button-jekyll-website.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - jekyll
  - flattr
  - microdonate
  - guide
  - money
  - revenue
  - monetize

---

![thumb](/images/flattr-logo.png)
Flattr is a free and simple way to earn money from blog posts. My Github hosted Jekyll website is being used primarily as a blog as you can see. By placing a small Flattr button at the end of each blog post, just above the comments section, I can ensure that visitors of my blog have an opportunity to thank me for the article. Now, step by step guide on how I did it.


<br>
**Step 1.** Sign up.

First, you need a Flattr account. Sign up for Flattr using the following link: [Flattr](https://flattr.com/signup)


<br>
**Step 2.** Create the template with Flattr Loader script.

Create a file called `flattr-script.html` in the `_includes` catalog of your Jekyll website. Insert the following content into that file:

```javascript
<script type="text/javascript">
    /* <![CDATA[ */
    (function() {
        var s = document.createElement('script');
        var t = document.getElementsByTagName('script')[0];

        s.type = 'text/javascript';
        s.async = true;
        s.src = '//api.flattr.com/js/0.6/load.js?'+
                    'mode=auto' +
                    '&html5-key-prefix=data-flattr';

        t.parentNode.insertBefore(s, t);
    })();
    /* ]]> */
</script>
```

This is a ready to use code. For further information see [Embedded buttons](http://developers.flattr.net/button/) on the Flattr docs.


<br>
**Step 3.** Create the template with Flattr button.

Create a file called `flattr-button.html` in the `_includes` catalog of your Jekyll website. Insert the following content into that file:

```html
{% raw %}
<a class="FlattrButton" style="display:none;"
    title="{{ page.title }}"
    data-flattr-uid="YOUR-USER-NAME"
    data-flattr-tags="{{ page.tags }}"
    data-flattr-category="text"
    data-flattr-language="{{ page.lang }}"
    data-flattr-button="compact"
    href="{{ site.url }}{{ page.url }}">
    {{ page.excerpt }}
</a>
{% endraw %}
```

Note: The `style="display:none;"` option needed to avoid that the embedded button definition is shown while the page is loading

Note: Replace the `YOUR-USER-NAME` with your own user name from your Fllatr account.

Note: The `data-flattr-category` variable can be set to any of the available categories: `text`, `images`, `video`, `audio`, `software`, `people`, `rest`.

Note: Since my blog supports both english and russian posts so I define a dynemic language attribute. If your Jekyll-website is written in one language only then replace the `{% raw %}{{ page.lang }}{% endraw %}` with your actual language code. All available language codes you can find [here](https://api.flattr.com/rest/v2/languages.txt).

Note: Decide which button you want to use – compact or classic. To switch to classic, all you need to do is deleting the `data-flattr-button="compact"` line completely.

Note: Make sure you’ve set `page.excerpt` via "Front Matter" on top of your posting. See the following example:

```
---
layout: post
lang: en_EN
title:  "This is the first post on my blog"
date:   2016-07-04 17:49:00
category: blogging
tags: "post, jekyll, blogging"
excerpt: "Teaser text ..."
---
```

<br>
**Step 4.** Call the flattr-script template from a default template.

Go into the `_layouts` catalog, find the `default.html` file and insert the following code right before the `</head>` tag:

```
{% raw %}{% include flattr-script.html %}{% endraw %}
```

This will ensure that the flattr-script template will be added to every page of your website.

Note: Some themes have a separeted file with head section (`<head></head>` tags). This file can be named `head.html` and be placed in the `_includes` catalog.

<br>
**Step 5.** Call the flattr-button template from a post template.

Go into the `_layouts` catalog and find the `post.html` file (or any layout file for which you would like Flattr button displayed) and insert the following code:

```
{% raw %}{% include flattr-button.html %}{% endraw %}
```

I place this right after the `{% raw %}{{ content }}{% endraw %}`, but the placements is totally up to you. In my case a Flattr buuton will be displayed at the end of each blog post, just above the comments section.

When everything went well, the flattr button should show up with the next page generation on activated posts. Now you’ve got Flattr buttons automatically add to all your post with the page excerpt on the Flattr page of your "thing".


<br>

#### Browser support

The buttons should support all modern browsers like the latest version of Firefox, Safari and Chrome and also Internet Explorer 8 and newer. It will degrade nicely in older browsers like Internet Explorer 7 – it will just not show.