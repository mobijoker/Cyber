---
lang: en
ref: custom-404-page-for-website-hosted-on-github
title: Custom 404 page for website hosted on GitHub
date: 2016-01-13T00:57:11+00:00
author: Arthur Gareginyan
layout: post
permalink: /developing/custom-404-page-for-website-hosted-on-github.html
categories:
  - Developing
tags:
  - 404
  - 404 page
  - 404.html
  - 404.md
  - github
  - github 404 page
  - github.com
  - not found

---

![thumb](/images/404-error-icon.png)
Recently I migrated my personal website to Adobe Muse and hosted it on GitHub Pages. Here it is: <a href="http://www.arthurgareginyan.com" target="_blank">arthurgareginyan.com</a>. Everything looks good. I tried to preserve my existing URLs. But the process wasn't perfect. So I created a custom 404 page. 
 

### Creating a 404 page

The GitHub Pages have a default template for display a 404 error page when people try to access nonexistent pages on your website. But you can create a custom 404 page in consistent with your Theme's style. All you need to do is create the page (the same as the others pages) with explanation of the situation, and then give the name of the file - `404.html`. GitHub will automatically use yours `404.html` file as the “page not found” page.

Now step by step:

**1.** Navigate to your GitHub Pages repository.

**2.** Switch to the master branch for a <a href="https://help.github.com/articles/user-organization-and-project-pages/#user--organization-pages" target="_blank">User/Organization Pages</a> website, or to the `gh-pages` branch for a <a href="https://help.github.com/articles/user-organization-and-project-pages/#project-pages" target="_blank">Project Pages</a> website.

**3.** Create a new HTML file named `404.html` at the root level of your GitHub Pages repository.

**4.** Add the content which explain the situation.

**5.** Commit your changes and, if you're working on a local clone of your repository, push them up to GitHub.

**Note:** If you want your Project Pages website to have a custom 404 page, you must use a custom domain.


### Content of the 404 page

You shouldn’t understate its utility. The 404 page is perhaps the most neglected web design element. When your website visitors land on your 404 error page, it can be everything from a major inconvenience to a pleasant surprise. While this page has the sole function of telling the user where to go next, the creation of your 404 page should be approached from both a creative and functional point of view.

I liked the design of 404 page from <a href="http://www.gog.com/error/404" target="_blank">Gog.com</a>. Here's their 404 page:
<img src="/images/404-example.png" alt="static contact form" width="1024" height="541" class="size-large wp-image-8834" />

This design is simple and allows for easy navigation through the menu. So I wanted to make a similar page for my website. Here's what I've got:
<img src="/images/404.png" alt="static contact form" width="1024" height="541" class="size-large wp-image-8835" />

You can check my 404 page at <a href="http://www.arthurgareginyan.com/error" target="_blank">http://www.arthurgareginyan.com/error</a>
