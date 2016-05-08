---
id: 7514
lang: ru
ref: increasing-the-upload_max_filesize
title: Увеличение upload_max_filesize
date: 2015-09-07T14:38:21+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=7514
permalink: /ru/linux/increasing-the-upload_max_filesize.html
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

![thumb](/images/php-logo.png)
По умолчанию размер загружаемого файла для PHP (и, соответственно, для WordPress) установлен в 2 MB, что вызывает проблемы при попытке загрузки файла большего размера. Выполните следующие шаги если вы получили такое сообщение:
<pre>The uploaded file exceeds the upload_max_filesize directive in php.ini</pre>


**Шаг 1.** Подключитесь к терминалу вашего вебсервера.

**Шаг 2.** Найдите файл `php.ini`:

```
sudo find / -name "php.ini"
```

Возможные варианты:

<pre>
/etc/php5/apache2/php.ini
/etc/php5/cli/php.ini
/etc/php5/fpm/php.ini
/etc/php5/cgi/php.ini
</pre>

**Шаг 3.** Откройте файл php.ini:

```
sudo nano /etc/php5/apache2/php.ini
```

**Шаг 4.** Найдите строку `upload_max_filesize = 2M` используя комбинацию клавиш `Ctrl+W`.

Вот она:

<pre>
; Maximum allowed size for uploaded files.
; http://php.net/upload-max-filesize
upload_max_filesize = 2M
</pre>

и замените её строкой с большим значением, например:

<pre>
; Maximum allowed size for uploaded files.
; http://php.net/upload-max-filesize
upload_max_filesize = 10M
</pre>

Сохраните изменения в файле (нажмите `Ctrl+O` для записи и `Ctrl+X` для выхода).

**Шаг 5.** Перезагрузите ваш вебсервер:

Для Apache:

```
sudo service apache2 restart
```

или Nginx:

```
sudo service nginx restart
```

Готово! Пробуйте снова загрузить файл.
