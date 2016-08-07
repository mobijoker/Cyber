---
title: Fixing Jekyll GitHub Metadata warning
ref: the-title-of-post
permalink: /web/the-title-of-post.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - monetize
  - 

---

![thumb](/images/xxx.png)

## Description

How to fix the error of Jelyll + GitHub Pages due to which is displayed the following message:

	GitHub Metadata: No GitHub API authentication could be found. Some fields may be missing or have incorrect data.

If you have recently upgraded to Jekyll v3.x.x then you may face GitHub Metadata warning (in your local development environment).

Here’s the solution to fix this warning:

This is what I did to resolve this problem:

<br>

---

## Causing

I ran local server by execute this command:

```
$> jekyll serve
```

I got this errors on the command line window.


## Create token

GitHub Metadata is a gem required by Jekyll. We need a GitHub personal token to make it work. Follow the excellent guide on GitHub to create a token, copy it to a safe place.


## Create environment variable

Now, create new environment variable in your system named `JEKYLL_GITHUB_TOKEN` with the value pasted from the created token. Open a new instance of command line and make sure this command displays correct information.

```
echo $JEKYLL_GITHUB_TOKEN
```

---------------------------------------------------------------------------

1. Create an GitHub access token with `public_repo` scope. (Remember to keep your tokens secret; treat them just like passwords!)

2. Now similarly as previous goto `Control Panel > System > Advances system settings` and click Environment Variables. Or simply type “environment variables” on Start menu search box.

3. Then define new user variable with variable name `JEKYLL_GITHUB_TOKEN` and GitHub access token as variable value (which is something like `abc123def456`).

4. Now click OK and Apply.

5. System reboot may needed to work for first time.

For security reason you can also access GitHub token with the following command line while building or serving Jekyll site:

```
JEKYLL_GITHUB_TOKEN=abc123def456 bundle exec jekyll serve
```

---

1. Create GitHub personal token ([guide](https://help.github.com/articles/creating-an-access-token-for-command-line-use/))

2. Add the `JEKYLL_GITHUB_TOKEN` environment variable whose content is the created token.


---

```
# Environment variables
export JEKYLL_GITHUB_TOKEN='abc123def456'
```