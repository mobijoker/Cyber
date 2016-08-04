---
lang: ru
ref: how-to-fix-every-call-to-the-add_setting-method-needs-to-have-a-sanitization
title: 'How to fix: "Every call to the add_setting() method needs to have a sanitization"'
date: 2015-07-31T05:09:29+00:00
author: Arthur Gareginyan
layout: post
permalink: /ru/web/how-to-fix-every-call-to-the-add_setting-method-needs-to-have-a-sanitization.html
switch_like_status:
  - 1
categories:
  - Error
  - Web
tags:
  - add_setting
  - error
  - plugin
  - required
  - sanitiz
  - sanitization
  - sanitization callback function
  - theme
  - theme check
  - theme update
  - wordpress
  - wp

---

![thumb](/images/error.png)
Некоторое время назад WordPress.org изменил правила публикации тем в их репозитории. И теперь, Я не имею возможности опубликовать обновление моей темы, из-за следующей ошибки:
 
<pre>
REQUIRED: Found a Customizer setting that did not have a sanitization callback function. Every call to the add_setting() method needs to have a sanitization callback function passed.
</pre>

Для локализации проблему я использовал <a href="https://wordpress.org/plugins/theme-check/" target="_blank">плагин "Theme Check"</a>. После установки страница плагина будет доступна в `"WordPress Dashbord" -> "Appearance" -> "Theme Check"`. Этот плагин не показывает больше информации чем wordpress.org при публикации обновления темы. Но мы можем модифицировать его, значит начнём.

Если <a href="https://wordpress.org/plugins/theme-check/" target="_blank">плагин "Theme Check"</a> ещё не установлен, то нужно сделать это.

А за тем модифицировать файл `customizer.php` находящийся в `plugins/theme-check/checks/`. Его можно модифицировать непосредственно из WordPress Dashbord. Для этого перейдите в `"WordPress Dashbord" -> "Plugins" -> "Editor"` и выбирете `"Theme Check"` плагин.

Теперь, в файл `customizer.php`, добавим такую строку:

```php
echo "$file_path: $match ";
```

После этого блока кода:

```php
if ( false === strpos( $match, 'sanitize_callback' ) && false === strpos( $match, 'sanitize_js_callback' ) ) {
$this->error[] = '<span class="tc-lead tc-required">' . __('REQUIRED','theme-check') . '</span>: ' . __( 'Found a Customizer setting that did not have a sanitization callback function. Every call to the <strong>add_setting()</strong> method needs to have a sanitization callback function passed.', 'theme-check' );
```

Готово. Это должно указать на файл и фрагмент кода вызывающего ошибку. В моём случае, оно показало эту строку:

<pre>
/var/www/site/wp-content/themes/anarcho-notepad/inc/customizer.php: 'copyright_post', array( 'default' => 'Copyright ©
</pre>

Эта строка значит то, что код вызывающий ошибку этот:

<pre>
'copyright_post', array( 'default' => 'Copyright ©
</pre>

и он находится в файле `customizer.php`. Значит нужно найти этот код в файле. Вот он:

```php
// Copyright after post
$wp_customize->add_setting( 'copyright_post', array(
	'default'			=> 'Copyright &copy; 2014. All rights reserved.',
	'sanitize_callback'	=> 'esc_attr',
));
```

Как вы видите `sanitize callback function` имеется. Проблема заключается в специальном символе `&copy;` в значении ключа `default`.

`&copy ; = Copyright = © = (c)`

Теперь Я должен изменить специальный символ `&copy ;` на его текстовую версию `(c)` или просто удалить его.
