---
title: 'WooCommerce: Remove the "Additional Information" Tab'
ref: woocommerce-remove-additional-information-tab
permalink: /web/woocommerce-remove-additional-information-tab.html
author: Arthur Gareginyan
lang: en
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

---

![thumb](/images/thumbnail/woocommerce.png)
Some of my WooCommerce clients didn’t want to show the “Additional Information” tab on the single product pages on their websites. There are 2 simple solutions: CSS one to hide this tab and PHP one to delete it completely. In this article I show you both solutions.


<br>
<br>

Before:
![](/images/woocommerce-remove-additional-information-tab/image-1.png)

After:
![](/images/woocommerce-remove-additional-information-tab/image-2.png)


## CSS solution

Input this code in your Custom CSS box or chiled stylesheet.
Add the following CSS snippet to `styles.css` file of your child theme or use the [My Custom Styles](https://wordpress.org/plugins/my-custom-styles/) plugin for better and easy management of all your CSS snippets.

```css
// Hide the additional information tab
li.additional_information_tab {
	display: none !important;
}
```


## PHP solution

Add the following PHP snippet to `functions.php` file of your child theme or use the [My Custom Functions](https://wordpress.org/plugins/my-custom-functions/) plugin for better and easy management of all your PHP snippets.

```php
// Remove the additional information tab
function woo_remove_product_tabs( $tabs ) {
    unset( $tabs['additional_information'] );
    return $tabs;
}
add_filter( 'woocommerce_product_tabs', 'woo_remove_product_tabs', 98 );
```

For more information see the [WooCommerce Docs](https://docs.woocommerce.com/document/editing-product-data-tabs/) page.