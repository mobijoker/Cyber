---
title: Добавление email формы подписки на блог при помощи Feedburner
ref: adding-email-subscription-form-blog-using-feedburner
permalink: /ru/web/adding-email-subscription-form-blog-using-feedburner.html
author: Arthur Gareginyan
translator: Arthur Gareginyan
lang: ru
layout: post
categories:
  - web
tags:
  - feedburner
  - subscription form
  - subscription
  - subscribe
  - email subscription
  - форма подписки
  - подписка
  - email подписка
  - подписка по эллектронной почте
  - поток
  - rss поток
  - rss лента
  - rss feed
  - rss
  - feed

---

![thumb](/images/adding-email-subscription-form-blog-using-feedburner/sign-up.png)
Отличный способ, чтобы быть в курсе новостей блога который ты любишь это подписаться на подписку по электронной почте на их посты. Таким образом, когда в блоге появится новый пост, он появится также прямо в твоём почтовом ящике. Если ты хочешь предложить такую опцию посетителям твоего вебсайта, это легко сделать. В этой статье я покажу тебе, как добавить на твой вебсайт форму подписки по электронной почте которая подключена к Feedburner.

<br>

Feedburner это веб-приложение для управления потоком вебсайта. В настоящее время он принадлежит Google, но больше не поддерживается Google-ом. Если ты настроишь поток с твоего вебсайта в Feedburner, то он будет изменять поток согласно твоим требованиям. Он также предоставляет статистику трафика и другие полезные статистические данные. В большинстве блогов в качестве способа подписки используется Feedburner.

Теперь шаг за шагом.


## **Шаг 1.** Поиск RSS потока

Прежде всего, нужно найти URL RSS поока твоего блога. Он должен выглядеть примерно как одна из них:

```
http://your-blog.com/rss
http://your-blog.com/feed.xml
```


## **Шаг 2.** Регистрация в Feedburner

Тебе нужен аккаунт в Feedburner. Feedburner один из инструментов Google, поэтому если у тебя уже есть основной аккаунт Google, который ты используешь для других служб, таких как Gmail, Google Drive, Google+ или YouTube, то ты можешь авторизоваться в Feedburner используя этот аккаунт Google. Иначе тебе нужно будет создать новый аккаунт.

Зарегистрируйся в Feedburner используя следующую ссылку: [Feedburner](http://feedburner.com/)


## **Шаг 3.** Настройка Feedburner

После входа в Feedburner, он предложит ввести URL RSS потока твоего блога который ты нашёл ранее.

![center](/images/adding-email-subscription-form-blog-using-feedburner/1.png)

На следующем экране тебе будет предложено ввести название для твоего потока, а также там ты сможешь настроить ссылку Feedburner.

![center](/images/adding-email-subscription-form-blog-using-feedburner/2.png)

На следующем экране тебе будет предложено либо нажать кнопку "Next" для того, чтобы добавить дополнительную Feedburner статистику в твой поток, либо пропустить вперёд для того, чтобы начать управление твоим потоком. Для целей данного руководства, выберите "Skip directly to feed management".

![center](/images/adding-email-subscription-form-blog-using-feedburner/3.png)

После того, как ты увидешь главный экран управления подачи, нажми на кнопку "Publicize" в верхней части экрана, выбери пункт меню "Email Subscriptions" в меню услуг слева и нажми на кнопку "Activate".

![center](/images/adding-email-subscription-form-blog-using-feedburner/4.png)

Feedburner предлагает два варианта опции подписки. Один из них это форма, а другой просто ссылка. Скопируй код формы для того, чтобы ты мог использовать его на следующем шаге.

![center](/images/adding-email-subscription-form-blog-using-feedburner/5.png)


## **Шаг 4.** Добавление email формы подписки в тему

Ты можешь поместить код формы в любом месте твоей темы где ты хочешь показать форму email подписки. 

Если твой блог основан на CMS WordPress, то ты можешь использовать "Text" виджет в боковой панели или нижнем колонтитуле (если твоя тема имеет такую опцию). Просто вставь код формы в область настройки виджета, сохрани изменения и готово!

Если ты не используешь CMS WordPress, то тебе нужно найти файл темы который отвечает за показ макета страницы по умолчанию на твоём вебсайта. В зависимости от веб-платформы (WordPress, Joomla, Jekyll и т.д.) этот файл может иметь имя `default.html`, `index.html` или другое.

> **Примечание:** Твоя тема может иметь отдельный файл для показа в боковой панели или нижнем колонтитуле. В этом случае тебе нужен файл который может иметь имя такое как `sidebar.html` и `footer.html` или `sidebar.php` и `footer.php`.

> **Примечание:** Ты можешь изменить все аспекты формы тем же способом, что при стилизации любой другой части темы твоего вебсайта.


<br>
Готово! Теперь твой вебсайт имеет форму подписки по электронной почте и посетители смогут подписаться на твой вебсайт используя свой адрес электронной почты. Теперь ты будешь иметь возможность управлять и видеть то сколько людей подписались на твой вебсайт через Feedburner.


## Форма подписки на моём блоге

Для отображения формы подписки по электронной почте на моём Jekyll блоге я выбрал раздел нижнего колонтитула. Я изменил код формы и добавил немного CSS стилей. Вот что у меня получилось:

```html
<div class="widget-subscribe">
    <h6 class="widget-footer-title">Subscribe</h6>
    <p>Subscribe to our Newsletter and get new posts delivered to your inbox - free!</p>
    <form action="https://feedburner.google.com/fb/a/mailverify" method="post" target="popupwindow" onsubmit="window.open('https://feedburner.google.com/fb/a/mailverify?uri=MyCyberUniverse', 'popupwindow', 'scrollbars=yes,width=550,height=520');return true">
        <input type="email" name="email" placeholder="Email address" class="subscribe-input">
        <input type="hidden" value="MyCyberUniverse" name="uri"/>
        <input type="hidden" name="loc" value="en_US"/>
        <button type="submit" value="Subscribe" name="subscribe" class="subscribe-button">Subscribe</button>
    </form>
</div>
```

```css
<style>
.widget-subscribe {
    float: right;
    width: 100%;
    padding-bottom: 30px;
}
.widget-footer-title {
    color: #fff;
    text-transform: uppercase;
    font-size: 14px;
    margin-bottom: 15px;
    font-weight: 700;
}
.subscribe-form {
    position: relative;
    margin-top: 10px;
}
.subscribe-input {
    
    box-sizing: border-box;
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
    border-radius: 4px;
    -moz-border-radius: 4px;
    -webkit-border-radius: 4px;
    background-color: #fff;
    width: -webkit-calc(100% - 130px );
    width: calc(100% - 130px );
    padding: 10px 40px 10px 10px;
    color: #999;
    font-size: 14px;
    line-height: normal;
}
.subscribe-button {
    position: relative;
    display: inline-block;
    top: -3px;
    font-family: Trajan Pro;
    font: 500 15px/15px 'Trajan Pro';
    text-transform: uppercase;
    text-align: center;
    vertical-align: middle;
    color: #fff;
    cursor: pointer;
    background: #19b4cf;
    padding: 14px 15px 10px 12px;
    border: 0;
    -webkit-border-radius: 3px;
    -moz-border-radius: 3px;
    border-radius: 3px;
    -webkit-box-shadow: 0px 3px 0px 0px #148ea4;
    -moz-box-shadow: 0px 3px 0px 0px #148ea4;
    box-shadow: 0px 3px 0px 0px #148ea4;
    -webkit-transition: color 0.3s, background 0.3s, box-shadow 0.3s, border-color 0.3s;
    -moz-transition: color 0.3s, background 0.3s, box-shadow 0.3s, border-color 0.3s;
    transition: color 0.3s, background 0.3s, box-shadow 0.3s, border-color 0.3s;
}
.subscribe-button:hover {
    background: #0093b1;
    -webkit-box-shadow: 0px 3px 0px 0px #0F7183;
    -moz-box-shadow: 0px 3px 0px 0px #0F7183;
    box-shadow: 0px 3px 0px 0px #0F7183;
}
</style>
```

Ты можешь использовать этот код на своём собственном вебсайте, но не забудьте изменить `MyCyberUniverse` на имя твоего потока в Feedburner.

<br>
Я надеюсь, что помог тебе настроить Feedburner для твоего вебсайта. Теперь, когда вы знаете как это работает, подпишитесь на мой блог. Спасибо за прочтение!
