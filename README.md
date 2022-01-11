# htaccess-301-redirect

## Woocommerce instructions for full removal of their plugin

> There are two things to understand when uninstalling or removing WooCommerce

- If you deactivate and delete the plugin from WordPress, you only remove the plugin and its files. Your settings, orders, products, pages, etc… will still exist in the database
- If you need to remove ALL WooCommerce data, including products, order data, etc., you need to be able to modify the site’s `wp-config.php` file before deactivating and deleting the plugin

> To fully remove all WooCommerce data from your WordPress site, open your site’s wp-config.php file. Scroll down until you fine the the bottom, add the following constant on its own line above the “That’s all, stop editing” comment.

```
define( 'WC_REMOVE_ALL_DATA', true );
/* That’s all, stop editing! Happy publishing. */ 
```

## Rediirect syntax

This is the basic format from CSS Tricks [301 Redirects article](https://css-tricks.com/snippets/htaccess/301-redirects/)  (Apache servers obly):

```
Redirect 301 /oldpage.html http://www.yoursite.com/newpage.html
Redirect 301 /oldpage2.html http://www.yoursite.com/folder/
```

On Siteground I have the following examples where Siteground added the `RedirectMatch` redirects from the redirect tool in cPanel:

```
RedirectMatch 301 /Blog/pet-services-blog/pet-business/online-business-listing-review-sites-pet-business/ /Blog/category/pet-services-blog/pet-business/
RedirectMatch 301 /oldpage2.html http://www.yoursite.com/folder/

Redirect 301 fairmountpetservice.com/index.html https://fairmountpetservice.com/Blog/index/
Redirect 301 /oldpage.html http://www.yoursite.com/newpage.html
```

Here are the pages I need to redirect:

```
https://twoaveragegamers.com/cart/
https://twoaveragegamers.com/cart-2/
https://twoaveragegamers.com/cart-3/
https://twoaveragegamers.com/checkout/
https://twoaveragegamers.com/checkout-2/
https://twoaveragegamers.com/checkout-3/
https://twoaveragegamers.com/my-account/
https://twoaveragegamers.com/my-account-2/
https://twoaveragegamers.com/my-account-3/

https://twoaveragegamers.com/shop/
https://twoaveragegamers.com/shop-2/
https://twoaveragegamers.com/shop-3/
```

Standard formatted 301's:

```
Redirect 301 /cart/ https://twoaveragegamers.com/
Redirect 301 /cart-2/ https://twoaveragegamers.com/
Redirect 301 /cart-3/ https://twoaveragegamers.com/
Redirect 301 /checkout/ https://twoaveragegamers.com/
Redirect 301 /checkout-2/ https://twoaveragegamers.com/
Redirect 301 /checkout-3/ https://twoaveragegamers.com/
Redirect 301 /my-account/ https://twoaveragegamers.com/
Redirect 301 /my-account-2/ https://twoaveragegamers.com/
Redirect 301 /my-account-3/ https://twoaveragegamers.com/

Redirect 301 /shop/ https://twoaveragegamers.com/
Redirect 301 /shop-2/ https://twoaveragegamers.com/
Redirect 301 /shop-3/ https://twoaveragegamers.com/
```

Thy the `RedirectMatch` replacement if it doesn't take:

```
RedirectMatch 301 /cart/ https://twoaveragegamers.com/
RedirectMatch 301 /cart-2/ https://twoaveragegamers.com/
RedirectMatch 301 /cart-3/ https://twoaveragegamers.com/
RedirectMatch 301 /checkout/ https://twoaveragegamers.com/
RedirectMatch 301 /checkout-2/ https://twoaveragegamers.com/
RedirectMatch 301 /checkout-3/ https://twoaveragegamers.com/
RedirectMatch 301 /my-account/ https://twoaveragegamers.com/
RedirectMatch 301 /my-account-2/ https://twoaveragegamers.com/
RedirectMatch 301 /my-account-3/ https://twoaveragegamers.com/

RedirectMatch 301 /shop/ https://twoaveragegamers.com/
RedirectMatch 301 /shop-2/ https://twoaveragegamers.com/
RedirectMatch 301 /shop-3/ https://twoaveragegamers.com/
```

Here are the redirects for my pet service site, both versions: https://fairmountpetservice.com/Blog/

```
https://fairmountpetservice.com/Blog/cart/
Redirect 301 /cart/ https://fairmountpetservice.com/Blog/
RedirectMatch 301 /cart/ https://fairmountpetservice.com/Blog/

https://fairmountpetservice.com/Blog/checkout/
Redirect 301 /checkout/ https://fairmountpetservice.com/Blog/
RedirectMatch 301 /checkout/ https://fairmountpetservice.com/Blog/

https://fairmountpetservice.com/Blog/my-account/
Redirect 301 /my-account/ https://fairmountpetservice.com/Blog/
RedirectMatch 301 /my-account/ https://fairmountpetservice.com/Blog/

https://fairmountpetservice.com/Blog/products/
Redirect 301 /products/ https://fairmountpetservice.com/Blog/
RedirectMatch 301 /products/ https://fairmountpetservice.com/Blog/
```

I had one already done with `RedirectMatch`: 

```
https://fairmountpetservice.com/Blog/shop/
RedirectMatch 301 /shop/ https://fairmountpetservice.com/Blog/
```
