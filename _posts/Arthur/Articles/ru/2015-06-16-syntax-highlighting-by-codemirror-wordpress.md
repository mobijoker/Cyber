---
lang: ru
ref: syntax-highlighting-by-codemirror-wordpress
title: 'Подсветка синтаксиса с CodeMirror и WordPress'
date: 2015-06-16
author: Arthur Gareginyan
translator: Arthur Gareginyan
layout: post
permalink: /ru/web/syntax-highlighting-by-codemirror-wordpress.html
switch_like_status:
  - 1
categories:
  - Web
tags:
  - codemirror
  - highlight
  - highlighter
  - highlighting
  - javascript
  - syntax
  - wordpress
  - подсветка кода
  - подсветка синтаксиса

---

![thumb](/images/thumbnail/CodeMirror.png)
О применении JavaScript библиотеки CodeMirror совместно с CMS WordPress
и её интеграции в WordPress проэкты (темы и плагины).


CodeMirror — это компонент JavaScript, который предоставляет редактор кода в браузере. Когда доступен модуль (mode) для нужного языка, то он будет раскрашивать ваш код (подсветки синтаксиса) и опционально помогать с отступом.


### Сборка CodeMirror

В начале нужно собрать каталог CodeMirror с нужными модулями и если надо темами и аддонами. Делается это просто. Для этого нужно скачать архив CodeMirror с сайта разработчика (<a href="http://codemirror.net" target="_blank">http://codemirror.net</a>) и удаляя из него лишнее оставить только нужное.

Минимально необходимый набор:

* Каталог `lib` с файлами `codemirror.js` и `codemirror.css`.
* Каталог `mode` с нужными модами (только js файлы).
* Каталоги `theme` и `addon` нужны в случае использования тем или аддонов.
* В случае публикации вашего проекта нужно использовать файлы `LICENSE` и `README.md`.

Я приведу пример подсветки синтаксиса языков HTML и PHP. А нужные вам моды вы можете определить на [этой странице](https://codemirror.net/mode/) руководства.

Понадобится ещё два файла (`config.js`, `customestyle.css`) о которых Я скажу позже.

Теперь всё это нужно разместить в каталоге с названием `codemirror` в корне проэкта. В результате собранный каталог должен выглядеть примерно так:

<pre>
codemirror-.
           |--lib--.
           |       |--codemirror.js
           |       '--codemirror.css
           |
           |--mode-.
           |       |--xml.js
           |       |--javascript.js
           |       |--css.js
           |       |--htmlmixed.js
           |       |--clike.js
           |       '--php.js
           |
           |--theme-.
           |        '--default.css
           |
           |--addon-.
           |        '--
           |
           |--LICENSE
           |--README.md
           |--config.js
           '--customestyle.css
</pre>


### Загрузка скриптов CodeMirror

Необходимо загрузить скрипты CodeMirror (те которые созданы в предыдущем пункте) в `header` страниц/ы. Для это в WordPress имеется cпециальная функция `_enqueue_scripts` загрузки скриптов и стилей в `header` страниц.

Пример загрузки скриптов с регистрацией:

```php
/**
 * Register and enqueue the CodeMirror scripts and styles
 */
function enqueue_codemirror_scripts($hook) {

    if ( 'appearance_page_my-custom-functions' != $hook ) {
        return;
    }

    // Registering scripts
    wp_register_script('codemirror', plugin_dir_url(__FILE__) . 'codemirror/lib/codemirror.js');
    wp_register_script('codemirror_xml', plugin_dir_url(__FILE__) . 'codemirror/mode/xml.js');
    wp_register_script('codemirror_javascript', plugin_dir_url(__FILE__) . 'codemirror/mode/javascript.js');
    wp_register_script('codemirror_css', plugin_dir_url(__FILE__) . 'codemirror/mode/css.js');
    wp_register_script('codemirror_htmlmixed', plugin_dir_url(__FILE__) . 'codemirror/mode/htmlmixed.js');
    wp_register_script('codemirror_clike', plugin_dir_url(__FILE__) . 'codemirror/mode/clike.js');
    wp_register_script('codemirror_php', plugin_dir_url(__FILE__) . 'codemirror/mode/php.js');
    wp_register_script('codemirror_config', plugin_dir_url(__FILE__) . 'codemirror/config.js');
    wp_register_style('codemirror_style', plugin_dir_url(__FILE__) . 'codemirror/lib/codemirror.css');
    wp_register_style('codemirror_customestyle', plugin_dir_url(__FILE__) . 'codemirror/customestyle.css');

    // Enqueue scripts
    wp_enqueue_script('codemirror');
    wp_enqueue_script('codemirror_xml');
    wp_enqueue_script('codemirror_javascript');
    wp_enqueue_script('codemirror_css');
    wp_enqueue_script('codemirror_htmlmixed');
    wp_enqueue_script('codemirror_clike');
    wp_enqueue_script('codemirror_php');
    wp_enqueue_script('codemirror_config');
    wp_enqueue_style('codemirror_style');
    wp_enqueue_style('codemirror_customestyle');

}
add_action( 'admin_enqueue_scripts', 'enqueue_codemirror_scripts' );
```

И без регистрации (если нет необходимости в регистрации):

```php
/**
 * Enqueue the CodeMirror scripts and styles
 */
function enqueue_codemirror_scripts($hook) {
    if ( 'appearance_page_my-custom-functions' != $hook ) {
        return;
    }

    wp_enqueue_script('codemirror', plugin_dir_url(__FILE__) . 'codemirror/lib/codemirror.js');
    wp_enqueue_script('codemirror_xml', plugin_dir_url(__FILE__) . 'codemirror/mode/xml.js');
    wp_enqueue_script('codemirror_javascript', plugin_dir_url(__FILE__) . 'codemirror/mode/javascript.js');
    wp_enqueue_script('codemirror_css', plugin_dir_url(__FILE__) . 'codemirror/mode/css.js');
    wp_enqueue_script('codemirror_htmlmixed', plugin_dir_url(__FILE__) . 'codemirror/mode/htmlmixed.js');
    wp_enqueue_script('codemirror_clike', plugin_dir_url(__FILE__) . 'codemirror/mode/clike.js');
    wp_enqueue_script('codemirror_php', plugin_dir_url(__FILE__) . 'codemirror/mode/php.js');
    wp_enqueue_script('codemirror_php', plugin_dir_url(__FILE__) . 'codemirror/config.js');
    wp_enqueue_style('codemirror_style', plugin_dir_url(__FILE__) . 'codemirror/lib/codemirror.css');
    wp_enqueue_style('codemirror_style', plugin_dir_url(__FILE__) . 'codemirror/customestyle.css');

}
add_action( 'admin_enqueue_scripts', 'enqueue_codemirror_scripts' );
```

Для плагина пути к скриптам указываются с помощью `plugin_dir_url()`:

<pre>
wp_enqueue_script( 'my_custom_script', plugin_dir_url( __FILE__ ) . 'myscript.js' );
</pre>

А для темы с помощью `get_template_directory_uri()`:

<pre>
wp_enqueue_script( 'my_custom_script', get_template_directory_uri( __FILE__ ) . 'myscript.js' );
</pre>

**Примечание:** `myscript.is` - это название нужного файла.

В зависимости от цели, скрипты можно загружать на всех страницах вэб-сайта, на всех страницах админки или на определённой странице.

Загрузка скриптов на всех страницах вэб-сайта:

```php
function enqueue_codemirror_scripts() {

    // Enqueue scripts
    ...

}
add_action( 'wp_enqueue_scripts', 'enqueue_codemirror_scripts' );
```

Загрузка скриптов на всех страницах админки:

```php
function enqueue_codemirror_scripts() {

    // Enqueue scripts
    ...

}
add_action( 'admin_enqueue_scripts', 'enqueue_codemirror_scripts' );
```

Загрузка скриптов на определённой странице (в моём примере это страница `edit.php`): 

```php
function enqueue_codemirror_scripts($hook) {
    if ( 'edit.php' != $hook ) {
        return;
    }

    // Enqueue scripts
    ...

}
add_action( 'admin_enqueue_scripts', 'enqueue_codemirror_scripts' );
```

**Примечание:** Название страницы можно увидеть в адресной строке.

Но если вам нужна страница темы то это будет немного сложнее. 

Название страницы темы можно определить по такой схеме:

<pre>
themes.php?page={page}
=>
appearance_page_{page}
</pre>

Тоесть, если адрес нужной страницы такой:

<pre>
themes.php?page=my-page.php
</pre>

То название будет `appearance_page_my-page`.


### Настройки

Вся настройка CodeMirror производится из конфигурационного файла `config.js`. Этот файл нужно создать и поместить в него следующее содержимое:

```js
// Configuration file for CodeMirror v1.0

  var myCodeMirror = CodeMirror.fromTextArea(document.getElementById('CodeMirror'), {
     lineNumbers: true,
     matchBrackets: true,
     mode: 'application/x-httpd-php',
     indentUnit: 4
  });
```

**Примечание:** Используется синтаксис JavaScript.

Настройки задаются в виде опций переменной `myCodeMirror`.

Значения опций из моего примера:

<pre>
lineNumbers: true, 				// Показывать номера строк.
matchBrackets: true,				// Подсвечивать парные скобки.
mode: "application/x-httpd-php",		// Режим подсветки.
indentUnit: 4 					// Размер табуляции (длина отступа в пробелах).
</pre>

Об остальных опциях можно узнать на странице руководства:
<a href="https://codemirror.net/doc/manual.html#config" target="_blank">https://codemirror.net/doc/manual.html#config</a>

**Примечание:** Строки с опциями, кроме последней, должны заканчиваться запятыми.


### Стили

Для применения своих стилей отображения нужно создать файл `customestyle.css`.

Пример содержания файла `customestyle.css`:

```css
  .CodeMirror {
     border: 1px solid cornflowerblue;
     height: auto;
  }
```

**Примечание:** Используется синтаксис CSS.


### Обрабатываемое поле

Теперь последний пункт. Нужно указать CodeMirror'у область для обработки кода. Это делается спомощью HTML тэга `<textarea>` (текстовое поле) с `id` - `CodeMirror`. Тоесть, на нужных страницах, подсвечиваемый код нужно обернуть в этот тэг, например так:

```html
<textarea cols="50" rows="10" id="CodeMirror" >
</textarea>
```


### Эпилог

Если весь код размесить на одной HTML странце то он будет выглядеть так:

```html
...
   <script src="codemirror/lib/codemirror.js"></script>
   <script src="codemirror/mode/xml.js"></script>
   <script src="codemirror/mode/javascript.js"></script>
   <script src="codemirror/mode/css.js"></script>
   <script src="codemirror/mode/htmlmixed.js"></script>
   <script src="codemirror/mode/clike.js"></script>
   <script src="codemirror/mode/php.js"></script>
   <link rel="stylesheet" href="codemirror/lib/codemirror.css">
   <link rel="stylesheet" href="codemirror/theme/default.css">
</head>
<body>
   <div id="container">
      <textarea cols="50" rows="10" id="code" ></textarea>
   </div>
   <script type="text/javascript" language="javascript">
     var myCodeMirror = CodeMirror.fromTextArea(document.getElementById('code'), {
        lineNumbers: true,
        matchBrackets: true,
        mode: 'application/x-httpd-php',
        indentUnit: 4
     });
   </script>
   <style>
     .CodeMirror {
        border: 1px solid cornflowerblue;
        height: auto;
     }
   </style>
</body>
</html>
…
```


### Ссылки

* Официальный сайт:
<a href="http://codemirror.net" target="_blank">http://codemirror.net</a>
* Официальный man:
<a href="http://codemirror.net/doc/manual.html" target="_blank">http://codemirror.net/doc/manual.html</a>
* Страница на GitHub:
<a href="https://github.com/codemirror/codemirror" target="_blank">https://github.com/codemirror/codemirror</a>
