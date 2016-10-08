---
lang: en
ref: increasing-the-upload_max_filesize
title: Increasing the upload_max_filesize
date: 2015-09-07
author: Arthur Gareginyan
layout: post
permalink: /linux/increasing-the-upload_max_filesize.html
categories:
  - Error
  - Linux
  - Web
tags:
  - /etc/php5/cgi/php.ini
  - /etc/php5/cli/php.ini
  - /etc/php5/fpm/php.ini
  - 2 mb
  - 2M
  - php.ini
  - upload_max_filesize
  - wordpress

---

![thumb](/images/thumbnail/php-logo.png)
The default upload file size for php (and, consequently, for WordPress) is 2 MB, which is a problem if you want to upload a files that’s bigger. Follow these steps if you get this message:
<pre>
The uploaded file exceeds the upload_max_filesize directive in php.ini
</pre>


**Step 1.** Connect to the terminal of your web sever.

**Step 2.** Locate the `php.ini` filer:

```sh
sudo find / -name "php.ini"
```

Examples of output:

<pre>
/etc/php5/apache2/php.ini
/etc/php5/cli/php.ini
/etc/php5/fpm/php.ini
/etc/php5/cgi/php.ini
</pre>

**Step 3.** Open a php.ini file:

```sh
sudo nano /etc/php5/apache2/php.ini
```

**Step 4.** Find the line `upload_max_filesize = 2M` by using `Ctrl+W` key combination.

That's it:

<pre>
; Maximum allowed size for uploaded files.
; http://php.net/upload-max-filesize
upload_max_filesize = 2M
</pre>

and replace it with a higher value, for example:

<pre>
; Maximum allowed size for uploaded files.
; http://php.net/upload-max-filesize
upload_max_filesize = 10M
</pre>

Save the changes to the file (press `Ctrl+O` to write out and `Ctrl+X` to exit).

**Step 5.** Restart your web server:

For Apache:

```sh
sudo service apache2 restart
```

or Nginx:

```sh
sudo service nginx restart
```

Done! Try the upload again.
