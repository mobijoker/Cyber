---
title: 'WooCommerce: Удаление закладки "Additional Information"'
ref: woocommerce-remove-additional-information-tab
permalink: /ru/web/woocommerce-remove-additional-information-tab.html
author: Arthur Gareginyan
translator: Arthur Gareginyan
lang: ru
layout: post
categories:
  - web
tags:
  - fix
  - how to fix
  - woocommerce
  - wordpress
  - product page
  - product tabs
  - single product page
  - additional information
  - additional information tab
  - extra informatie
  - extra informatie field
  - extra informatie tab
  - remove tab
  - hide tab
  - скрыть закладку
  - убрать закладку
  - удалить закладку
  - страница продукта
  - закладки продукта
  - страница товара
  - закладки товара
  - дополнительная информация

---

![thumb](/images/thumbnail/woocommerce.png)
Некоторые из моих WooCommerce клиентов не хотят чтобы вкладка "Дополнительная информация" показывалась на отдельных страницах продуктов на их веб-сайте. Есть 2 простых решения: CSS решение для того, чтобы скрыть эту вкладку и PHP решение для того, чтобы удалить её полностью. В этой статье я покажу вам оба решения.


<br>
<br>

До:
![](/images/woocommerce-remove-additional-information-tab/image-1.png)

После:
![](/images/woocommerce-remove-additional-information-tab/image-2.png)


## CSS решение

Добавь следующий CSS код в `style.css` файл твоей дочерней темы или используй [My Custom Styles](https://wordpress.org/plugins/my-custom-styles/) плагин для лучшего и более удобнового управления всеми твоими CSS кодами на веб-сайте.

```css
// Hide the additional information tab
li.additional_information_tab {
	display: none !important;
}
```


## PHP решение

Добавь следующий PHP код в `functions.php` файл твоей дочерней темы или используй [My Custom Functions](https://wordpress.org/plugins/my-custom-functions/) плагин для лучшего и более удобнового управления всеми твоими PHP кодами на веб-сайте.

```php
// Remove the additional information tab
function woo_remove_product_tabs( $tabs ) {
    unset( $tabs['additional_information'] );
    return $tabs;
}
add_filter( 'woocommerce_product_tabs', 'woo_remove_product_tabs', 98 );
```

Для получения дополнительной информации смотри страницу [WooCommerce Docs](https://docs.woocommerce.com/document/editing-product-data-tabs/).