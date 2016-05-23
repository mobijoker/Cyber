---
id: 676
lang: en
ref: upgrading-the-svn-working-copy-to-new-version
title: Upgrading the SVN working copy to new version
date: 2015-08-08T23:33:39+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=676
permalink: /linux/upgrading-the-svn-working-copy-to-new-version.html
categories:
  - Debian/Ubuntu
  - Linux
  - Mac OS
  - Raspberry Pi
tags:
  - checkout
  - E155036
  - repository
  - svn
  - svn error
  - upgrade
  - working copy is too old

---

![thumb](/images/SubVersion.png)
Today I upgraded the Subversion on my computer from 1.6 to 1.7 version. Subversion version 1.7 has a new repository structure and requires to upgrade all existing working copies.


If we attempt to use Subversion 1.7 on a working copy created with an older version of Subversion, then we will see the following error:

```
svn status
```

<pre>
svn: E155036: Please see the 'svn upgrade' command
svn: E155036: Working copy '/home/user/project' is too old (format 10, created by Subversion 1.6)
</pre>

We need to use the `svn upgrade` command to upgrade the working copy to the most recent metadata format supported by the new version of Subversion.

```
svn upgrade [PATH TO PROJECT]
```

<pre>
Upgraded '.'
Upgraded 'A'
Upgraded 'A/B'
Upgraded 'A/B/E'
</pre>

Now my working copy is upgraded!

**Note:** The `svn upgrade` command need to do for every SVN working copy.

**Note:** After upgrading to Subversion 1.7, you cannot go back to Subversion 1.6. And upgraded working copies will be unusable by older versions of Subversion.

**Note:** The `svn upgrade` command may take a while, and for some users, it may be more practical to simply checkout a new working copy.
