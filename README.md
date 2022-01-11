# htaccess-301-redirect

This is the basic format from CSS Tricks [301 Redirects article](https://css-tricks.com/snippets/htaccess/301-redirects/)  (Apache servers obly):

```
Redirect 301 /oldpage.html http://www.yoursite.com/newpage.html
Redirect 301 /oldpage2.html http://www.yoursite.com/folder/
```

On Siteground I have the following:

```
RedirectMatch 301 /Blog/pet-services-blog/pet-business/online-business-listing-review-sites-pet-business/ /Blog/category/pet-services-blog/pet-business/
Redirect 301 fairmountpetservice.com/index.html https://fairmountpetservice.com/Blog/index/
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

Standard ormatted 301's:

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
