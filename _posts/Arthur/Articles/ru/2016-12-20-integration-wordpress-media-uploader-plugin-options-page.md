---
title: 'Интеграция WordPress медия загрузчика в страницу настроек плагина'
ref: integration-wordpress-media-uploader-plugin-options-page
permalink: /ru/integration-wordpress-media-uploader-plugin-options-page.html
author: Arthur Gareginyan
translator: Milena Kiseleva
lang: ru
layout: post
categories:
  - development
tags:
  - wordpress
  - plugin
  - плагин
  - plug-in
  - plugin creation
  - создание плагина
  - wordpress plugin
  - wordpress плагин
  - плагин wordpress
  - options page
  - wordpress options page
  - media uploader
  - wordpress media uploader
  - image uploader
  - загрузчик изображений
  - wordpress image uploader
  - wordpress загрузчик изображений
  - picture uploader
  - wordpress picture uploader
  - wordpress uploader 
  - медиа загрузчик
  - wordpress медиа загрузчик
  - wordpress загрузчик

---

![thumb](/images/integration-wordpress-media-uploader-plugin-options-page/1.png)
Иногда Я хочу создать простой и интуитивно понятный графический интерфейс для моих клиентов, для того, чтобы дать им возможность загружать изображения на странице настроек моего плагина. Я мог бы сделать только поле ввода текста, где они могут поместить URL изображения и иногда это то, что мне нужно в той или иной ситуации, но чаще так делать не профессионально. Я хочу иметь довольных клиентов, Я хочу сделать удобный интерфейс моих плагинов. В этой статье Я покажу тебе то, как интегрировать красивый, простой и настраиваемый WordPress медия загрузчика (WordPress Media Uploader) в страницу настроек плагина.


<br><br>

> **Примечание:** Эта инструкция сфокусирована на загрузке изображений на странице настроек плагина. Если ты не знаешь как создать страницу настроек плагина то Я рекомендую тебе в первую очередь взглянуть на инструкции по WordPress Settings API.


## Что мы будем делать и что мы получим?

![](/images/integration-wordpress-media-uploader-plugin-options-page/1.png)

* В нашу форму мы добавим кнопку для загрузки изображений в файловую систему сервера и другую кнопку для удаления этого изображения.

* Мы создадим поле для предварительного просмотра изображения. Пользователь всегда должен видеть вещи, происходящие на экране. Для пользователя не достаточно загрузить изображение и перейти на страницу для того, чтобы проверить есть ли изображение.

* Мы будем использовать WordPress Media Uploader для загрузки изображения или выбора уже существующего в медиатеке, так нам не придётся беспокоиться о всём процессе. Мы также будем управлять загрузкой изображения в правильную папку и прикрепим его к WordPress Media Library.

* У нас будет возможность удалить и файл изображения и его версию прикреплённую к WordPress Media Library.



## Демонстрация

В качестве примера Я использую страницу настроек одного из моих плагинов. Вот как кнопка выглядит на странице настроек моего WP плагина [RSS Fees Icon](https://wordpress.org/plugins/rss-feed-icon/):

![](/images/integration-wordpress-media-uploader-plugin-options-page/2.png)

> **Примечание:** Ты можешь стилизовать его, как ты захочешь при помощи CSS кода.

При нажатии на кнопку "Загрузить", появится pop-up окно WordPress медиа загрузчика.

![](/images/integration-wordpress-media-uploader-plugin-options-page/3.png)
![](/images/integration-wordpress-media-uploader-plugin-options-page/4.png)

В этом окне ты можешь выбрать одно из предыдущих загруженных изображений или загрузить новое. Нажми на кнопку "Insert into post" и ты увидишь это:

![](/images/integration-wordpress-media-uploader-plugin-options-page/5.png)

Теперь мы готовы отправить форму и сохранить URL изображения в базе данных.



## Руководство

Настало время для того, чтобы создать страницу настроек плагина, создать форму на ней и добавить её в Админ Панель. Как Я говорил ранее, цель этого руководства не заключается в том, чтобы описать то, как создать страницу настроек плагина, так что Я не буду объяснять то, как это сделать.


### Шаг 1. Код PHP 

Мы собираемся создать функцию PHP (мы назовём её `arthur_image_uploader`) который будет динамически создавать HTML код для Media Uploader:


```php
/**
 * Image Uploader
 * 
 * author: Arthur Gareginyan www.arthurgareginyan.com
 */
function arthur_image_uploader( $name, $width, $height ) {

    // Set variables
    $options = get_option( 'RssFeedIcon_settings' );
    $default_image = plugins_url('img/no-image.png', __FILE__);

    if ( !empty( $options[$name] ) ) {
        $image_attributes = wp_get_attachment_image_src( $options[$name], array( $width, $height ) );
        $src = $image_attributes[0];
        $value = $options[$name];
    } else {
        $src = $default_image;
        $value = '';
    }

    $text = __( 'Upload', RSSFI_TEXT );

    // Print HTML field
    echo '
        <div class="upload">
            <img data-src="' . $default_image . '" src="' . $src . '" width="' . $width . 'px" height="' . $height . 'px" />
            <div>
                <input type="hidden" name="RssFeedIcon_settings[' . $name . ']" id="RssFeedIcon_settings[' . $name . ']" value="' . $value . '" />
                <button type="submit" class="upload_image_button button">' . $text . '</button>
                <button type="submit" class="remove_image_button button">&times;</button>
            </div>
        </div>
    ';
}
```

> **Примечание:** Ты можешь изменить URL изображения, которое будет отображаться по умолчанию (10-ая сторка, переменная `$default_image`).

> **Примечание:** Измени имя параметра на своё собственное (9-ая и 30-ая строки, `RssFeedIcon_settings `). В этом примере Я использую setting в которой Я сохраняю массив, а не просто одну переменную.

Помести эту функцию в главный PHP файл твего плагина. Теперь остаётся только использовать его на странице настроек плагина. Просто вызови эту функцию с некоторыми переменными изнутри формы:

```
arthur_image_uploader( 'custom_image', $width = 115, $height = 115 );
```

> **Примечание:** `custom_icon` - Это имя твоего option который будет сохранён в базу данных MySQL.



### Шаг 2. Код jQuery 

Теперь нужен jQuery код для того, чтобы Media Uploader работал правильно. Для этого просто помести следующий jQuery код в JavaScript файл твоего плагина.

```js
// The "Upload" button
$('.upload_image_button').click(function() {
	var send_attachment_bkp = wp.media.editor.send.attachment;
	var button = $(this);
	wp.media.editor.send.attachment = function(props, attachment) {
		$(button).parent().prev().attr('src', attachment.url);
		$(button).prev().val(attachment.id);
		wp.media.editor.send.attachment = send_attachment_bkp;
	}
	wp.media.editor.open(button);
	return false;
});

// The "Remove" button (remove the value from input type='hidden')
$('.remove_image_button').click(function() {
	var answer = confirm('Are you sure?');
	if (answer == true) {
		var src = $(this).parent().prev().attr('data-src');
		$(this).parent().prev().attr('src', src);
		$(this).prev().prev().val('');
	}
	return false;
});
```

> **Примечание:** Если в твоём плагине нет файла JavaScript, то создай пустой файл `admin.js` в папке плагина и подключи его к странице настроек плагина используя `wp_enqueue_script()` из главного PHP файла твоего плагина. Затем помести jQuery код (тот, что выше) в этот JavaScript файл.


Это всё. Теперь мы можем использовать WordPress Медиа Uploader на нашей странице настроек плагина.

Если у тебя есть вопросы или есть какие-либо предложения по улучшению, пожалуйста, пиши в комментарии.
