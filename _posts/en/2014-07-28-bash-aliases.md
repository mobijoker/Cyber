---
lang: en
ref: bash-aliases
title: BASH aliases
date: 2014-07-28T15:56:39+00:00
author: Arthur Gareginyan
layout: post
permalink: /linux/bash-aliases.html
categories:
  - DD-WRT
  - Debian/Ubuntu
  - Linux
  - Raspberry Pi
tags:
  - alias
  - aliases
  - apt
  - apt-get
  - bash
  - bash_aliases
  - bash_profile
  - bashrc

---

![thumb](/images/terminal-300x300.png)
You can create shortened commands by using aliases. Aliases are very convenient to use for frequently used commands.

For example:

* `sudo apt-get upgrade` can be shortened to `apt upgrade`.
* `sudo apt-get install` can be shortened to `apt install`.
* `sudo apt-get remove` can be shortened to `apt remove`.
* `sudo apt-get update && sudo apt-get upgrade && sudo apt-get autoremove && sudo apt-get autoclean` can be shortened to `update`.


### Begin

Assuming you are using Bash, create a `.bash_aliases` file in your users home directory, if it already doesn't exist:

```
touch ~/.bash_aliases
```

Open up your `.bash_aliases` :

```
nano ~/.bash_aliases
```

Then, add a lines with the following to the file:

<pre>
alias apt='sudo apt-get'
alias update='sudo apt-get update && sudo apt-get upgrade && sudo apt-get autoremove && sudo apt-get autoclean'
</pre>

To apply the changes immediately to your bash profile without having to log out, simply run this:

```
. ~/.bashrc
```

or :

```
. ~/.bash_profile
```

Now you can install any new package with the syntax:

```
apt install <package-name>
```

Remember, because `sudo` has been added to your alias, you don’t have to type it every time. It will prompt you to use the password the first time, and won’t ask again for the duration of the defined timeout period.

Do note that autocompletion will not work with the alias.

Although these examples have been geared towards Debian and Ubuntu, you can obviously use aliases on any Unix-like operating system. The technique of applying them just varies depending on the shell environment you are using.

If the `~/.bash_aliases` file does not work, then add aliases to the end of `~/.bashrc` or `~/.bash_profile`. For example, in Mac OS X you must create `~/.bash_profile` file and then add the aliases.
