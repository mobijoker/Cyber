---
title: Fixing the Jekyll + GitHub Metadata warning
ref: fixing-jekyll-github-metadata-warning
permalink: /web/fixing-jekyll-github-metadata-warning.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - jekyl
  - github pages
  - error
  - warning
  - github metadata
  - github API authentication
  - github token
  - JEKYLL_GITHUB_TOKEN

---

![thumb](/images/error.png)
When I run the `jekyll serve` command in my local Jekyll environment I got the following warning:
<pre>
GitHub Metadata: No GitHub API authentication could be found. Some fields may be missing or have incorrect data.
</pre>

<br>

Here’s the solution to fix this warning:

**Step 1.** Create the GitHub personal access token with `public_repo` scope. You can find guide [here](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).

![](/images/github-metadata-error.png)

**Note:** Remember to keep the token secret - you don’t want other people to use the API on your behalf!

<br>
**Step 2.** Open the `~/.bash_profile` file (you can use your favorite text editor instead of `nano` if you’d like).

```sh
nano ~/.bash_profile
```

**Note:** This file may have different names and locations depending on your shell and OS. For example: `.profile`, `.bashrc`, `.zshenv`. In MacOS is a `.bash_profile` that loacated at user home directory (`~/`). You can search in Google for information about file in your OS in wich you can add a new environment variable.

<br>
**Step 3.** Then define new environment variable with variable name `JEKYLL_GITHUB_TOKEN` and GitHub access token as variable value (which is something like `abc123def456`). You can do this by add the following line to a new blank line:

```
export JEKYLL_GITHUB_TOKEN='abc123def456'
```

**Note:** Replace the `abc123def456` with your token.

<br>
**Step 4.** Now reload the Terminal.

You can check the new environment variable with the following command line that should display your GitHub token.

```sh
echo $JEKYLL_GITHUB_TOKEN
```

### In addition

For security reason you can also access GitHub token with the following command line while building or serving Jekyll website:

```sh
JEKYLL_GITHUB_TOKEN=abc123def456 bundle exec jekyll serve
```

Also you can set temporary environment variable with the following command line:

```sh
export JEKYLL_GITHUB_TOKEN=abc123def456
```

The `export` command run by itself and not contained within `.bash_profile` will only be a temporary setting and the environment variable will not persist unless you add it to the `.bash_profile`.
