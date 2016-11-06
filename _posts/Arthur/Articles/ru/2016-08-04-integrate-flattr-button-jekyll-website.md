---
title: Интеграция кнопки Flatr в веб-сайт на Jekyll
ref: integrate-flattr-button-jekyll-website
permalink: /ru/web/integrate-flattr-button-jekyll-website.html
author: Arthur Gareginyan
translator: Milena Kiseleva
lang: ru
layout: post
categories:
  - web
tags:
  - jekyll
  - flattr
  - microdonate
  - guide
  - money
  - revenue
  - monetize
  - монетизация
  - прибыль
  - деньги
  - инструкция
  - микродонаты
  - микродонейты
  - зарабаток

---

![thumb](/images/thumbnail/flattr-logo.png)
Flattr это бесплатный и простой способ заработать деньги с блога. Как вы можете видеть мой Jekyll веб-сайт размещённый в Github используется в основном как блог. Разместив маленькую кнопку Flattr в конце каждого поста в блоге, чуть выше раздела комментариев, Я могу быть уверенным в том, что посетители моего блога имеют возможность поблагодарить меня за статью. Далее пошаговая инструкция о том, как это сделать.


<br>
**Step 1.** Регистрация.

Во-первых тебе нужен аккаунт Flattr. Зарегестрируйся во Flattr используя следующую ссылку: [Flattr](https://flattr.com/signup)


<br>
**Step 2.** Создание шаблона с Flattr Loader script.

Создай файл с именем `flattr-script.html` в `_includes` каталоге твоего Jekyll веб-сайта. Вставь следующее содержимое в этот файл:

```javascript
<script type="text/javascript">
    /* <![CDATA[ */
    (function() {
        var s = document.createElement('script');
        var t = document.getElementsByTagName('script')[0];

        s.type = 'text/javascript';
        s.async = true;
        s.src = '//api.flattr.com/js/0.6/load.js?'+
                    'mode=auto' +
                    '&html5-key-prefix=data-flattr';

        t.parentNode.insertBefore(s, t);
    })();
    /* ]]> */
</script>
```

Это полностью готовый к использованию код. Для получения дополнительной информации смотри [Embedded buttons](http://developers.flattr.net/button/) на странице документации Flattr.


<br>
**Step 3.** Создание шаблона с кнопкой Flattr.

Создай файл с именем `flattr-button.html` в `_includes` каталоге твоего Jekyll веб-сайта. Вставь следующее содержимое в этот файл:

```html
{% raw %}
<a class="FlattrButton" style="display:none;"
    title="{{ page.title }}"
    data-flattr-uid="YOUR-USER-NAME"
    data-flattr-tags="{{ page.tags }}"
    data-flattr-category="text"
    data-flattr-language="{{ page.lang }}"
    data-flattr-button="compact"
    href="{{ site.url }}{{ page.url }}">
    {{ page.excerpt }}
</a>
{% endraw %}
```

Примечание: Опция `style="display:none;"` нужна для того, чтобы избежать показа кнопки во время загрузки страницы.

Примечание: Замени `YOUR-USER-NAME` на твоё собственное имя из аккаунта Fllatr.

Примечание: Переменная `data-flattr-category` может быть установлена в любую из доступных категорий: `text`, `images`, `video`, `audio`, `software`, `people`, `rest`.

Примечание: Так как посты на моём блоге доступны на двух языках (английском и русском) то Я установил динамический аттрибут языка. Если посты на твоём Jekyll веб-сайте написаны только на одном языке то замени `{% raw %}{{ page.lang }}{% endraw %}` кодом актуального для вас языка. Все доступные коды языков можешь найти [здесь](https://api.flattr.com/rest/v2/languages.txt).

Примечание: Реши какую кнопку ты хочешь использовать - компактную или классическую. Чтобы переключиться на классическую, всё что тебе нужно это полностью удалить строку`data-flattr-button="compact"`.

Примечание: Убедись, что ты установил `page.excerpt` через "Front Matter" в верхней части твоего поста. Смотри следующий пример:

```
---
layout: post
lang: en_EN
title:  "This is the first post on my blog"
date:   2016-07-04 17:49:00
category: blogging
tags: "post, jekyll, blogging"
excerpt: "Teaser text ..."
---
```

<br>
**Step 4.** Вызов шаблона flattr-script из основного шаблона блога.

Перейди в каталог `_layouts`, найди фаил `default.html` и вставь следующий код прямо перед тегом `</head>`:

```
{% raw %}{% include flattr-script.html %}{% endraw %}
```

Благодаря этому шаблон flattr-script будет добавлен к каждой странице твоего веб-сайта.

Примечание: Некоторые темы имеют отделенный файл с `head` секцией (`<head></head>` теги). Этот файл может называться например `head.html` и распологаться в каталоге `_includes`.

<br>
**Step 5.** Вызов шаблона flattr-button из шаблона поста.

Перейди в каталог `_layouts` и найди файл `post.html` (или любой другой файл макета в который ты хочешь встроить кнопку Flattr) и вставь следующий код:

```
{% raw %}{% include flattr-button.html %}{% endraw %}
```

Я разместил этот код сразу после `{% raw %}{{ content }}{% endraw %}`, но место размещения полностью зависит от тебя. В моём случае копка Flattr будет показываться в конце каждого поста в блоге, чуть выше секции с комментариями.

Если всё сделано правильно, то кнопка flattr должна появится на активированых страницах после следующей генерацией страниц. Теперь кнопки Flattr будут автоматически добавлятся ко всем постам с кратким содержанием на Flattr странице твоих "thing".


<br>

#### Поддержка браузерами

Кнопки должны поддерживать все современные браузеры, такие как последняяи версии Firefox, Safari, Chrome а также Internet Explorer 8 и новее. В старых браузерах, таких как Internet Explorer 7 - кнопки просто не будут показываться.
