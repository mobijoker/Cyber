---
lang: en
ref: configuring-a-godaddy-domain-name-with-github-pages
title: Configuring a GoDaddy domain name with GitHub pages
date: 2015-12-31T14:26:30+00:00
author: Arthur Gareginyan
layout: post
permalink: /web/configuring-a-godaddy-domain-name-with-github-pages.html
categories:
  - Web
tags:
  - domain
  - domain name
  - github
  - github pages
  - godaddy
  - pages

---

![thumb](/images/configuring-a-godaddy-domain-name-with-github-pages/icon.png)
GitHub Pages is an incredibly simple, user-friendly solution for hosting a simple personal website. By default the address will be `username.github.io`. Below, I'll explain how I set up my github.io user page with my own domain name arthurgareginyan.com that registered trough GoDaddy.com.


### Step 1. Set up your github.io user page and register a domain name

I'll assume this is done. In my case, I set up a user page at `arthurgareginyan.github.io`. When I navigated to that page, the URL stayed as arthurgareginyan.github.io (i.e., it didn't redirect to anywhere). Also, through GoDaddy.com, I registered the domain name `arthurgareginyan.com`. Now I want to point the custom domain name (in my case is - `arthurgareginyan.com`) to my GitHub page.


### Step 2. Commit the CNAME file to GitHub page

**a)** Login to your GitHub Account.

**b)** Go to the root of your page directory, in my case is - `arthurgareginyan.github.io`.

**c)** Create a new file named `CNAME` (all caps, no extension).

**d)** Put the domain name in your file, in my case is - `www.arthurgareginyan.com` (without `http://`, only apex domain `arthurgareginyan.com` or with subdomain like `www.`).

<img src="/images/configuring-a-godaddy-domain-name-with-github-pages/screenshot-1.png" alt="github & godaddy" />

**e)** Commit and push your changes.

**Note:** You can use a subdomain `www.` together with an apex domain. This is configured using the CNAME file. For example:

* If your CNAME file contains `example.com`, then `www.example.com` will redirect to `example.com`.
* If your CNAME file contains `www.example.com`, then `example.com` will redirect to `www.example.com`.


**Note:** By similar way you can add the file `robots.txt` to your GitHub page. 


### Step 3. Configure the DNS in GoDaddy

**a)** Login to your GoDaddy Account.

**b)** Go to "Manage Your Domains".

**c)** Choose the domain name that you want to point to your github.io page.

**d)** Click on the "DNS Zone File" tab.
<img src="/images/configuring-a-godaddy-domain-name-with-github-pages/screenshot-2.png" alt="github & godaddy" />

**e)** Under the "A (Host)" section add a two A-records:

* First: "A (Host)" record with `host` = `@` and `Points to` = `192.30.252.153`.
* Second: "A (Host)" record with `host` = `@` and `Points to` = `192.30.252.154`.


<img src="/images/configuring-a-godaddy-domain-name-with-github-pages/screenshot-3.png" alt="github & godaddy" />

This is explained [there](https://help.github.com/articles/tips-for-configuring-an-a-record-with-your-dns-provider/).

**f)** Under the "CName (Alias)" section add a "CNAME (Alias)" record with `host` = `www` and `Points to` = `username.github.io` (in my case is `arthurgareginyan.github.io`).

<img src="/images/configuring-a-godaddy-domain-name-with-github-pages/screenshot-4.png" alt="github & godaddy" />

**g)** Save changes.

That's all I did with GoDaddy. I didn't change anything else, including the Nameserver (NS) records.


### Step 4. Testing

Changes require some time and do not take effect immediately. Patiently wait for your DNS settings to update. It can take up to 48 hours.

When the DNS updates, you should be able to navigate to your custom domain and see your `username.github.io` page, but now with custom domain name.

You can check your work with the following command:

```bash
dig arthurgarginyan.com +nostats +nocomments +nocmd
```

<pre>
;arthurgarginyan.com
arthurgarginyan.com.   73  IN  A 192.30.252.153
arthurgarginyan.com.   73  IN  A 192.30.252.154
</pre>

Congratulations, now you know how to add the custom domain name (URL) to GitHub pages. You can check my GitHub page at <a href="http://arthurgareginyan.com" target="_blank">http://arthurgareginyan.com</a>.
