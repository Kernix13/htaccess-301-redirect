# htaccess-301-redirect

## Woocommerce instructions for full removal of their plugin

> There are two things to understand when uninstalling or removing WooCommerce

- If you deactivate and delete the plugin from WordPress, you only remove the plugin and its files. Your settings, orders, products, pages, etc… will still exist in the database
- If you need to remove ALL WooCommerce data, including products, order data, etc., you need to be able to modify the site’s `wp-config.php` file before deactivating and deleting the plugin

> To fully remove all WooCommerce data from your WordPress site, open your site’s `wp-config.php` file. Scroll down until you fine the the bottom, add the following constant on its own line above the “That’s all, stop editing” comment.

```php
define( 'WC_REMOVE_ALL_DATA', true );
/* That’s all, stop editing! Happy publishing. */ 
```
** HUGE NOTE**: You have to have the plugin installed before you add the code to `wp-config.php`. Then when you deactivate the plugin and remove it the cod will run and remove everything (see bottom of this file).

## Redirect syntax

Is Bluehost running on Apache or a different server?

This is the basic format from CSS Tricks [301 Redirects article](https://css-tricks.com/snippets/htaccess/301-redirects/)  (Apache servers only):

```apacheconf
Redirect 301 /oldpage.html http://www.yoursite.com/newpage.html
Redirect 301 /oldpage2.html http://www.yoursite.com/folder/
```

On Siteground I have the following examples where Siteground added the `RedirectMatch` redirects from the redirect tool in cPanel:

```apacheconf
RedirectMatch 301 /Blog/pet-services-blog/pet-business/online-business-listing-review-sites-pet-business/ /Blog/category/pet-services-blog/pet-business/
RedirectMatch 301 /oldpage2.html http://www.yoursite.com/folder/

Redirect 301 fairmountpetservice.com/index.html https://fairmountpetservice.com/Blog/index/
Redirect 301 /oldpage.html http://www.yoursite.com/newpage.html
```

**Note**: My redirects are placed directly above the comment:

```apacheconf
# BEGIN WordPress
```

And I have this commented line before the start of my redirects:

```apacheconf
## WOOCOMMERCE AND STRIPE MANUAL REDIRECTS ##
```

Here are example redirects for my pet service site (both versions), though I used `RedirectMatch`:

```apacheconf
Redirect 301 /cart/ https://fairmountpetservice.com/Blog/
RedirectMatch 301 /cart/ https://fairmountpetservice.com/Blog/

Redirect 301 /checkout/ https://fairmountpetservice.com/Blog/
RedirectMatch 301 /checkout/ https://fairmountpetservice.com/Blog/

Redirect 301 /my-account/ https://fairmountpetservice.com/Blog/
RedirectMatch 301 /my-account/ https://fairmountpetservice.com/Blog/

Redirect 301 /products/ https://fairmountpetservice.com/Blog/
RedirectMatch 301 /products/ https://fairmountpetservice.com/Blog/
```

I had one already done with `RedirectMatch`: 

```apacheconf
RedirectMatch 301 /shop/ https://fairmountpetservice.com/Blog/
```

## Bluehost Nameservers

In case they are needed:

```
ns1.bluehost.com	162.88.60.37
ns2.bluehost.com	162.88.61.37
```

## The deactivation code

Here is the [Woocommerce Github code](https://github.com/woocommerce/woocommerce/blob/master/uninstall.php) for the snippet added to `wp-config.php`.

Looks like the uninstall.php file is doing the following things:

1. Unschedules all events attached to woo hooks using wp_clear_scheduled_hook starting on line 15
2. Dropping Woocommerce admin tables using ::drop_tables() on line 31
3. Removing "roles + caps" using ::remove_roles() on line 36 
4. Trashing pages using wp_trash_post( get_option ( 'various woocommerce page id names' ) ) starting on line 39
5. doing something with attributes if there are tables prefixed with woocommerce_... starting on line 48
6. dropping woo tables again, this time I assume for the plugin as opposed to the admin area on line 55 
7. delete woo records in the options table lines 58 & 59
8. delete woo records in the usermeta table line 62 
9. delete posts and data (posts, postmeta, comments, commentsmeta) starting on line 65
10. conditional delete of taxonomies & attributes if > WP version 4.2, line 75 (2 lines directly below): 
11. foreach delete of term taxonomies line 77
12. foreach delete of term attributes line 87
13. delete orphan records, terms, and term meta line 96
14. wp_cache_flush line 109

## MySQL queries to check for Woocommerce fields

SQL examples to find woocommerce fields in the `options` table:

```sql
SELECT * FROM `wpaa_options` WHERE option_name LIKE 'woocommerce\_%' OR option_name LIKE 'widget\_woocommerce\_%'
SELECT * FROM `wpaa_options` WHERE option_name LIKE 'woocommerce\_%'
SELECT * FROM `wpaa_options` WHERE option_name LIKE 'widget\_woocommerce\_%'
```

The last 2 SQL statements are just to run individual queries, but then you proabably know that if you know how to run queries in phpmyadmin. I had 127 records in total when I ran the combined query. Then I commented out the snippet in `wp-config.php`, installed Woo, un-commented the code in config, and finally deactivated and removed Woo. I ran the query again and it returned **ZERO** records.

Here is an example of SQL statements to manually delete the recor from the `options` table:

```sql
DELETE * FROM `wpaa_options` WHERE option_name LIKE 'woocommerce\_%' OR option_name LIKE 'widget\_woocommerce\_%'
DELETE * FROM `wpaa_options` WHERE option_name LIKE 'woocommerce\_%'
DELETE * FROM `wpaa_options` WHERE option_name LIKE 'widget\_woocommerce\_%'
```



So the removal process ran the code snippet in the config file most likely because it is hooking onto the deactivation and removal of the plugin. If you remove the plugin before adding the coee snippet then there is nothing to hook onto.

## IMPORTANT NOTE

**IF YOU INTENT TO INSTALL WOOCOMMERCE AFTER DOING THIS REMOVAL PROCESS, YOU WILL HAVE TO REMOVE THE 301 REDIRECTS FROM YOUR HTACCESS FILE OR THE PAGES WILL NEVER LOAD!!!!**
