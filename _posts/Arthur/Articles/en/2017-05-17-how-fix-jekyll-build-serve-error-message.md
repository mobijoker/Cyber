---
title: 'How to fix: Jekyll build/serve error message'
ref: how-fix-jekyll-build-serve-error-message
permalink: /web/how-fix-jekyll-build-serve-error-message.html
author: Arthur Gareginyan
lang: en
layout: post
categories:
  - web
tags:
  - how to
  - tutorial
  - jekyll
  - jekyll error
  - error
  - issue
  - problem
  - jekyll build
  - jekyll serve
  - bundler
  - bundle exec
  - bundle exec jekyll build
  - bundle exec jekyll serve

---

![thumb](/images/thumbnail/error.png)
We can set up a local version of our Jekyll GitHub Pages website to preview our website before making the changes public. But when I run the `jekyll [build | serve]` command it throws the following error message:

```
$ jekyll serve
Ignoring RedCloth-4.3.0 because its extensions are not built.  Try: gem pristine RedCloth --version 4.3.0
Ignoring rdiscount-2.2.0.1 because its extensions are not built.  Try: gem pristine rdiscount --version 2.2.0.1
Ignoring redcarpet-3.3.4 because its extensions are not built.  Try: gem pristine redcarpet --version 3.3.4
/Library/Ruby/Gems/2.0.0/gems/bundler-1.11.2/lib/bundler/runtime.rb:34:in `block in setup': You have already activated colorator 1.1.0, but your Gemfile requires colorator 0.1. Prepending `bundle exec` to your command may solve this. (Gem::LoadError)
	from /Library/Ruby/Gems/2.0.0/gems/bundler-1.11.2/lib/bundler/runtime.rb:19:in `setup'
	from /Library/Ruby/Gems/2.0.0/gems/bundler-1.11.2/lib/bundler.rb:92:in `setup'
	from /Library/Ruby/Gems/2.0.0/gems/jekyll-3.2.1/lib/jekyll/plugin_manager.rb:36:in `require_from_bundler'
	from /Library/Ruby/Gems/2.0.0/gems/jekyll-3.2.1/exe/jekyll:9:in `<top (required)>'
	from /usr/local/bin/jekyll:22:in `load'
	from /usr/local/bin/jekyll:22:in `<main>'
```


## What causes this problem

This error message means that we haven’t properly set up the Jekyll dependencies (gems and their versions) in our system. To solve this issue, follow the steps below.


## How to solve it

The best way to eliminate these errors is to solve each gems and their versions issues separately. But there is also the easiest way to solve this issue, it's just use the [Bundler](http://bundler.io). 

About: [Bundler](http://bundler.io) provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed. Bundler is an exit from dependency hell, and ensures that the gems you need are present in development, staging, and production. Starting work on a project is as simple as bundle install.

Getting started with Bundler is easy, just run this command:

```
gem install bundler
```

and then within the directory of our website, run this:

```
bundle install
```

Finally, we able to build and serve the website locally with the following command:

```
bundle exec jekyll serve
```

Now our website was successfully being served locally at `http://127.0.0.1:4000/` using the built-in web server provided by Jekyll.
