---
lang: ru
ref: ustanovka-na-sayt-favicon
title: Установка на сайт Favicon
date: 2013-06-20
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/web/ustanovka-na-sayt-favicon.html
categories:
  - Web
tags:
  - favicon
  - wordpress

---

![thumb](/images/thumbnail/favicon.jpg)
Из <a href="http://ru.wikipedia.org/wiki/Favicon">Wiki</a>:
“Favicon (сокр. от англ. FAVorites ICON — «значок для избранного», от названия папки с закладками в <a href="http://ru.wikipedia.org/wiki/Internet_Explorer">MSIE</a>) — значок веб-сайтаили веб-страницы. Отображается браузером в адресной строке перед URL страницы, а также в качестве картинки рядом с закладкой, во вкладках и в других элементах интерфейса.”


Для favicon необходимо изображение в формате `ico`, `png` или `gif` с размерами `16x16`, `32x32`, `48x48` или `64x64` и с 8-битной или 24-битной глубиной цвета.

Тип `image/x-icon` устарел в 2003 году после стандартизации типа для `ico`. Правильный тип `image/vnd.microsoft.icon` поддерживается всеми браузерами. Важно помнить, что иконка не будет показываться в браузере если её `Content-type`, возвращаемый веб-сервером, не совпадёт с указанным в html-коде страницы.

Можно указать несколько изображений в разных форматах — например, строку с `rel="shortcut icon"` и значком в формате `ico` для Internet Explorer, и строку `сrel="icon"` и значком в формате `gif` или `png` для остальных браузеров.


### Создание Favicon

Favicon можно создать разными способами. Есть специальные онлайн-сервисы, называемые favicon-генераторами, в которых можно в пару кликов создать favicon из картинки или же нарисовать его в специальном простеньком редакторе. Можно создать качественный favicon в Gimp или Photosop. Можно даже сделать favicon анимированным.

Вот пара примеров онлайн-сервисов по созданию favicon:

* <a href="http://www.favicon.cc/">http://www.favicon.cc/</a>
* <a href="http://favicon.ru/">http://favicon.ru/</a>

Мне понравился онлайн-сервис <a href="http://www.favicon.co.uk/">http://www.favicon.co.uk</a>, так как он делает из картинки более детализированные favicon нежели предыдущие сервисы. Для этого нужно выбрать “Favicon Size:  64x64”.

	
### Установка Favicon на сайт

Установить favicon на сайт я предлагаю правкой одного из двух файлов темы, `header.php` или `functions.php`.


#### Правка header.php
	
**1.** Подклачаемся к сайту по FTP.
	
**2.** Помещаем наш favicon в корень сайта (рядом с папками `wp-admin`, `wp-content` и `wp-includes`). Имя должно быть `favicon.ico`, `favicon.png` или `favicon.gif` в зависимости от расширения. Оно может быть и любым другим но в таком случае придётся править код вставляемый в файл.

**3.** Открываем для редактирования `header.php` и перед закрывающим тегом пишем:

Если `favicon.ico`:

```html
<!-- Favicon -->
	<link href="/favicon.ico" rel="shortcut icon" type="image/x-icon" />
	<link href="/favicon.ico" rel="icon" type="image/x-icon" />
<!-- Конец - Favicon -->
```

Если `favicon.gif`:

```html
<!-- Favicon -->
	<link href="favicon.ico" rel="shortcut icon" type="image/gif" /> 
	<link href="favicon.gif" rel="icon" type="image/gif" />
<!-- Конец - Favicon -->
```

А таким способом можно использовать favicon расположенный в другом месте и с другим именем. В том числе так можно грузить favicon даже с другого сайта.

Если `ico`:

```html
<!-- Favicon -->
	<link href="http://Ваш сайт/название картинки.ico" rel="shortcut icon" />
	<link href="http://Ваш сайт/название картинки.ico" rel="icon" type="image/x-icon" />
<!-- Конец - Favicon -->
```

Если gif:

```html
<!-- Favicon -->
	<link href="http://Ваш сайт/название картинки.gif" rel="shortcut icon" />
	<link href="http://Ваш сайт/название картинки.gif" rel="icon" type="image/gif" />
<!-- Конец - Favicon -->
```

#### Правка functions.php

**1.** Подклачаемся к сайту по FTP.

**2.** Помещаем наш favicon в корень сайта (рядом с папками `wp-admin`, `wp-content` и `wp-includes`). Имя должно быть `favicon.ico`, `favicon.png` или `favicon.gif` в зависимости от расширения. Оно может быть и любым другим но в таком случае придётся править код вставляемый в файл.

**3.** Открываем для редактирования functions.php и в конце, перед закрывающим тегом `?>` пишем:

Если `favicon.ico`:

```php
/* Favicon */
function my_favicon() {
	echo '	<link href="'.get_bloginfo('wpurl').'/favicon.ico" rel="shortcut Icon" type="image/x-icon" />';
}
 add_action('wp_head', 'my_favicon');
 add_action('admin_head', 'my_favicon');
 add_action('login_head', 'my_favicon' );
/* Конец - Favicon*/
```

Если `favicon.gif`:

```php
/* Favicon */
function my_favicon() {
	echo '	<link href="'.get_bloginfo('wpurl').'/favicon.gif" rel="shortcut Icon" type="image/gif" />';
}
 add_action('wp_head', 'my_favicon');
 add_action('admin_head', 'my_favicon');
 add_action('login_head', 'my_favicon' );
/* Конец - Favicon*/
```

**Примечание:** В вашей теме может не оказаться файла `header.php` или `functions.php`. В таком случае нужно вставлять код в файл `index.php` перед закрывающим тегом .
