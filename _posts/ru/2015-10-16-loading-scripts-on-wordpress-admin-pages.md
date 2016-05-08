---
id: 8693
lang: ru
ref: loading-scripts-on-wordpress-admin-pages
title: 'Загрузка скриптов на админ страницах WordPress'
date: 2015-10-16T09:28:48+00:00
author: Arthur Gareginyan
layout: post
guid: http://mycyberuniverse.com/?p=8693
permalink: /ru/web/loading-scripts-on-wordpress-admin-pages.html
categories:
  - Web
tags:
  - action hook
  - admin_enqueue_scripts
  - certain admin page
  - cms wordpress
  - enqueue
  - hook
  - load
  - loading
  - plugin
  - register
  - script
  - scripts
  - settings page
  - specific admin page
  - wordpress
  - wp_enqueue_scripts

---

![thumb]()
Иногда вам может понадобится создать отдельный файл стилей или JavaScript файл для страницы настройки вашего плагина, вместо вставки его в существующий код этой страницы. Но как загрузить этот скрипт только на страницах настройки плагина или темы (только на некоторых страницах `/wp-admin`)?


Для загрузки таблицы стилей или JavaScript файла в `head` раздел (заголовок/header) админ страниц/ы мы можем использовать `admin_enqueue_scripts` или `wp_enqueue_scripts` хук действия.

В зависимости от цели мы можем загружать скрипты на всех страницах веб-сайта, на всех страницах панели администратора или на конкретной странице панели администратора.

**1.** Загрузить скрипты везде на вашем веб сайте:

```
function enqueue_my_scripts() {
 
    // ENQUEUE SCRIPTS…
 
}
add_action( 'wp_enqueue_scripts', 'enqueue_my_scripts' );
```

**2.** Загрузить скрипты на всех страницах панели администратора:

```
function enqueue_my_scripts() {
 
    // ENQUEUE SCRIPTS…
 
}
add_action( 'admin_enqueue_scripts', 'enqueue_my_scripts' );
```

**3.** Загрузить скрипты на определённой странице меню верхнего уровня в панели администратора (в примере `edit.php` - “Записи”):

```
function enqueue_my_scripts($hook) {
    if ( 'edit.php' != $hook ) {
        return;
    }
 
    // ENQUEUE SCRIPTS…
 
}
add_action( 'admin_enqueue_scripts', 'enqueue_my_scripts' );
```

**4.** Загрузить скрипты на определённой странице из подменю в панели администратора.

Пример:

```
function enqueue_my_scripts($hook) {
    if ( 'appearance_page_my-page' != $hook ) {
        return;
    }
 
    // ENQUEUE SCRIPTS…
 
}
add_action( 'admin_enqueue_scripts', 'enqueue_my_scripts' );
```

В этом примере используется страница настройки расположенная в подменю раздела «Внешний вид» и эта страница имеет `menu-slug` `my-page`.

Для использования этого метода необходимо определить имя страницы. Название страницы, которое видно в адрес баре не подходит для этого.

Имя страницы в разделе «Внешний вид» можно определить по следующей схеме:
<pre>themes.php?page={page menu-slug}
=>
appearance_page_{page menu-slug}</pre>

`appearance_page_` это префикс для страниц в этом разделе меню. Вам нужно добавить префикс к `menu-slug`. Тоесть, если адрес нужной страницы  `themes.php?page=my-page.php`, то название будет `appearance_page_my-page`. С другими разделами панели администратора нужно сделать то же самое, но с другим префиксом. Раздел меню «Параметры» имеет префикс `settings_page_`. Если вы не можете найти правильное имя страницы вашего плагина то сделайте следующее.

Временно добавьте эту функцию в основной файл вашего плагина:

```
function enqueue_my_scripts($hook) {
    echo "<p style='text-align:center;'>" .$hook. "</p>";
}
add_action('admin_enqueue_scripts', 'enqueue_my_scripts');
```

После этого вы увидите текстовую строку под верхним админ-баром. Там будет написано правильное имя страницы вашего плагина. Вы можете скопировать это имя и затем удалить эту функцию.
