---
lang: ru
ref: add-social-media-buttons-to-your-website
title: 'Добавление кнопок социальных медиа на ваш вебсайт'
date: 2015-09-06T15:23:50+00:00
author: Arthur Gareginyan
layout: post
permalink: /ru/web/add-social-media-buttons-to-your-website.html
categories:
  - Web
tags:
  - button
  - icon
  - social media
  - social media buttons
  - social media icons
  - social media profile
  - social network
  - значки
  - значки социальных сетей
  - иконки
  - иконки социальных сетей
  - кнопки
  - кнопки социальных сетей
  - социальные медиа
  - социальные сети

---

![thumb](/images/social-media-icons.png)
Социальные медиа кнопки дают вам возможность использовать иконку популярных социальных сетей в которых содержится ссылки на ваши профили в социальных медиа. Вы узнаете о том как добавить вертикальную и горизонтальную линию или линии социальных медиа кнопок в запись, боковую панель или футер вашего вебсайта, используя иконки какие вам нравятся.


Пример того как это выглядит:
<img src="/images/social-media-icons-2.png" alt="social media icons-2" width="600" height="206" class="aligncenter size-full" />

Social Media Buttons Toolbar displayed below the content of a post (Twenty Sixteen theme) :
<img src="/images/screenshot-4-1.png" alt="WP plugin &quot;Social Media Buttons Toolbar&quot; by Arthur Gareginyan" width="1024" height="541" class="size-large wp-image-8794" />

Social Media Buttons Toolbar displayed in the sidebar using a shortcode in text widget (Twenty Sixteen theme) :
<img src="/images/screenshot-5.png" alt="WP plugin &quot;Social Media Buttons Toolbar&quot; by Arthur Gareginyan" width="1024" height="541" class="size-large wp-image-8795" />

Social Media Buttons Toolbar displayed in the footer using a simple call the function directly from theme file (vCard theme) :
<img src="/images/screenshot-7.png" alt="WP plugin &quot;Social Media Buttons Toolbar&quot; by Arthur Gareginyan" width="1024" height="541" class="size-large wp-image-8797" />

Social Media Buttons Toolbar displayed in the footer using a shortcode in text widget (Anarcho Notepad theme):
<img src="/images/screenshot-6.png" alt="WP plugin &quot;Social Media Buttons Toolbar&quot; by Arthur Gareginyan" width="379" height="359" class="size-large wp-image-8796" />

Кнопки располагаются горизонтально и в центре. Если они не поместятся в одну строку, то будут растянуты на несколько строк.

Вы можете добавить социальные медия кнопки на ваш вебсайт или блог двумя способами, но сначала вам понадобятся иконки.
 
 
### Подготовка

Поиск, скачивание и загрузка иконок на ваш вебсайт

**Шаг 1.** В интернете найдите социальные медиа иконки которые вы желаете испольщовать. Убедитесь в том, что вы не нарушаете авторских прав. Когда вы найдёте те которые вам нравятся, скачайте их на компьютер.

Я использую <a href="https://www.iconfinder.com/iconsets/social-buttons-2" target="_blank">“Social Buttons 2”</a> набор иконок от Ivlichev Victor Petrovich. Этот набор иконок бесплатный и находится под лицензией Creative Commons (Attribution 3.0 Unported).

**Шаг 2.** Поместите все иконки в новую папку, например `social-media-icons` и загрузите их в медиа библиотеку вашего вебсайта. В CMS WordPress это папка с названием `uploads` (она расположена в `/you-website/wp-content/uploads/`). Теперь адрес ведущий к вашим иконкам будет таким:
`http://your-website.com/wp-content/uploads/social-media-icons/facebook.ico`.


### Первый способ добавить социальные медиа кнопки

Первый способ добавить социальные медиа кнопки это использование "Text Widget".

**Шаг 1.** Перейдите в административную панель вашего вебсайта. Добавьте Text Widget в боковую панель или футер вашего вебсайта.

**Шаг 2.** Добавьте в "Text Widget" HTML код подобный следующему (Я использую этот код):

```
Следуйте за мной в социальных сетях::
<ul class="social-icons">
	<li>
		<a href="https://www.facebook.com/arthur.gareginyan" target='blank'>
			<img src="/images/social-media-icons/facebook.png" alt="Facebook" />
		</a>
	</li>
	<li>
		<a href="https://twitter.com/AGareginyan" target='blank'>
			<img src="/images/social-media-icons/twitter.png" alt="Twitter" />
		</a>
	</li>
	<li>
		<a href="http://instagram.com/arthur_gareginyan" target='blank'>
			<img src="/images/social-media-icons/instagram.png" alt="Instagram" />
		</a>
	</li>
	<li>
		<a href="https://plus.google.com/+ArthurGareginyan" target='blank'>
			<img src="//mycyberuniverse.com/wp-content/uploads/social-media-icons/google.png" alt="Google+" />
		</a>
	</li>
	<li>
		<a href="https://www.youtube.com/channel/UCvQenE1DumnZy1k5sTvgmSA" target='blank'>
			<img src="/images/social-media-icons/youtube.png" alt="YouTube" />
		</a>
	</li>
	<li>
		<a href="http://oneberserk.blogspot.ru" target='blank'>
			<img src="/images/social-media-icons/blogger.png" alt="Blogger" />
		</a>
	</li>
	<li>
		<a href="http://www.linkedin.com/in/arthurgareginyan" target='blank'>
			<img src="/images/social-media-icons/linkedin.png" alt="Linkedin" />
		</a>
	</li>
	<li>
		<a href="https://github.com/ArthurGareginyan" target='blank'>
			<img src="/images/social-media-icons/github.png" alt="Github" />
		</a>
	</li>
	<li>
		<a href="http://codepen.io/berserkr/" target='blank'>
			<img src="/images/social-media-icons/codepen.png" alt="Codepen" />
		</a>
	</li>
	<li>
		<a href="mailto:arthurgareginyan@gmail.com?subject=Message from mycyberuniverse.com" target='blank'>
			<img src="/images/social-media-icons/mail.png" alt="Mail" />
		</a>
	</li>
	<li>
		<a href="http://mycyberuniverse.com/feed" target='blank'>
			<img src="/images/social-media-icons/rss.png" alt="RSS Feed" />
		</a>
	</li>
</ul>
<style>
.social-icons {
    text-align: center;
}
.social-icons li {
    display:inline-block;
    list-style-type:none;
    -webkit-user-select:none;
    -moz-user-select:none;
}
.social-icons li a {
    border-bottom: none;
}
.social-icons li img {
    width:70px;
    height:70px;
    margin-right: 20px;
}
</style>
```

Как вы видите, код выше состоит из двух частей. Первая часть это список из ссылок к вашим профилям в социальных сетях и ваши иконки:

```
<ul>
	<li>
		…
	</li>
</ul>
```

Замените все мои ссылки на ваши ссылки на которые должны вести кнопки. Убедитесь в том, что ссылки начинаются с `http://` или `https://`.

Вторая часть это стили для ваших кнопок:

```
<style>
	…
</style>
```

Так же вы можете использовать этот способ для отображения ваших социальных медиа кнопок в записи.


### Второй способ добавить социальные медиа кнопки

Второй способ добавить социальные медиа кнопки это создание php функции для отображения кнопок в любом месте вашего вебсайта при помощи шорткода. Для этого нужно будет использовать `functions.php` файл вашей темы или использовать <a href="https://wordpress.org/plugins/my-custom-functions/" target="_blank">плагин “My Custom Functions”</a>.

**Шаг 1.** Мы будем использовать код подобный тому, что использовали в первом способе, но закроем код в функцию. Добавьте HTML код тому, что приведён ниже в `functions.php` файл вашей темы или в плагин:

```
/* SOCIAL MEDIA BUTTONS
************************************/
function my_social_media_icons(){
ob_start();
?>
</br>
Follow me on social media:
<ul class="social-icons">
	<li>
		<a href="https://www.facebook.com/arthur.gareginyan" target='blank'>
			<img src="/images/social-media-icons/facebook.png" alt="Facebook" />
		</a>
	</li>
	<li>
		<a href="https://twitter.com/AGareginyan" target='blank'>
			<img src="/images/social-media-icons/twitter.png" alt="Twitter" />
		</a>
	</li>
	<li>
		<a href="http://instagram.com/arthur_gareginyan" target='blank'>
			<img src="/images/social-media-icons/instagram.png" alt="Instagram" />
		</a>
	</li>
	<li>
		<a href="https://plus.google.com/+ArthurGareginyan" target='blank'>
			<img src="//mycyberuniverse.com/wp-content/uploads/social-media-icons/google.png" alt="Google+" />
		</a>
	</li>
	<li>
		<a href="https://www.youtube.com/channel/UCvQenE1DumnZy1k5sTvgmSA" target='blank'>
			<img src="/images/social-media-icons/youtube.png" alt="YouTube" />
		</a>
	</li>
	<li>
		<a href="http://oneberserk.blogspot.ru" target='blank'>
			<img src="/images/social-media-icons/blogger.png" alt="Blogger" />
		</a>
	</li>
	<li>
		<a href="http://www.linkedin.com/in/arthurgareginyan" target='blank'>
			<img src="/images/social-media-icons/linkedin.png" alt="Linkedin" />
		</a>
	</li>
	<li>
		<a href="https://github.com/ArthurGareginyan" target='blank'>
			<img src="/images/social-media-icons/github.png" alt="Github" />
		</a>
	</li>
	<li>
		<a href="http://codepen.io/berserkr/" target='blank'>
			<img src="/images/social-media-icons/codepen.png" alt="Codepen" />
		</a>
	</li>
	<li>
		<a href="mailto:arthurgareginyan@gmail.com?subject=Message from mycyberuniverse.com" target='blank'>
			<img src="/images/social-media-icons/mail.png" alt="Mail" />
		</a>
	</li>
	<li>
		<a href="http://mycyberuniverse.com/feed" target='blank'>
			<img src="/images/social-media-icons/rss.png" alt="RSS Feed" />
		</a>
	</li>
</ul>
<style>
.social-icons {
    text-align: center;
}
.social-icons li {
    display:inline-block;
    list-style-type:none;
    -webkit-user-select:none;
    -moz-user-select:none;
}
.social-icons li a {
    border-bottom: none;
}
.social-icons li img {
    width:70px;
    height:70px;
    margin-right: 20px;
}
</style>
</br>
<?php
$output = ob_get_clean();
return $output;
}
add_shortcode('my_social_media_icons', 'my_social_media_icons'); // Create shortcode
add_filter('widget_text', 'do_shortcode');  // Allow shortcodes in widgets
```

Сторка `add_shortcode(` создаёт шорткод `[my_social_media_icons]`.
Сторка `add_filter(` нужна для разрешения шорткодов в виджетах.

И теперь вы можете использовать шорткод `[my_social_media_icons]`. Просто довать этот шорткод в любое место вашего вебсайта, как пос, боковая панель или футер и ваши социальные медиа кнопки будут отображены.

**P.S.**
Если вы используете другую CMS вместо WordPress тогда вам нужно удалить строки создания шорткода и фильтр:

```
add_shortcode('my_social_media_icons', ‘my_social_media_icons');
add_filter('widget_text', 'do_shortcode');
```

Вместо использования шорткода вам нужно использовать следующий код для отображения кнопок:

```
<?php my_social_media_icons(); ?>
```
