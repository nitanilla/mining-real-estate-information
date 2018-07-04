=== Storefront Sticky Add to Cart ===
Contributors: jameskoster, woothemes
Tags: woocommerce, ecommerce, storefront, sticky
Requires at least: 4.0
Tested up to: 4.9.1
Stable tag: 1.1.8
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Storefront Sticky Add to Cart adds a convenient bar which sticks to the top of your product pages so that visitors can easily find and click the add to cart button.

== Description ==

Product pages can be long. Some products have long descriptions, lots of reviews, galleries, you name it. By the time a visitor has read all of the product content and decided to commit to purchasing the product, the add to cart button is often hidden way off screen at the top of the page. Not any more! The Storefront Sticky Add to Cart plugin reveals a small content bar at the top of the browser window which includes the product name, price, rating, stock status and the all-important add to cart button. It subtly slides into view once the standard add-to-cart button has scrolled out of view. Now when your customers decide they want to buy your product they no longer have to go hunting to add it to their cart!

[youtube https://www.youtube.com/watch?v=v3daZU1kWJs]

As the name suggests this plugin has been designed to work with our [Storefront](http://wordpress.org/themes/storefront/) theme. The add-to-cart bar colors will be lifted from your Storefront configuration in the Customizer. The main background color is applied to the background, the main text color applied to the text and the main link color applied to links. If you want to use this plugin with another theme you'll have to build your own integration. More info in the FAQ.

== Installation ==

1. Upload `storefront-sticky-add-to-cart` to the `/wp-content/plugins/` directory
2. Activate the plugin through the 'Plugins' menu in WordPress
3. Done!

== Frequently Asked Questions ==

= I want to integrate with a theme other than Storefront, how do I do it? =

It's very simple, most of the core styles are loaded regardless. You'll just need to apply a background color to the content bar like so; `.ssatc-sticky-add-to-cart { background-color: white; }`.

= Why doesn't he sticky add to cart component display on mobile? =

It simply takes up too much valuable screen real estate. You can display it on mobile with a few lines of css if you need to.

== Screenshots ==

1. The sticky add to cart bar in action.

== Changelog ==

= 1.1.8 - 20.12.2017 =
* Fix - Undefined index error for specific stock settings.

= 1.1.7 - 27.10.2017 =
* Tweak - Use wp_kses_post() for stock availability sanitization. Ensures compatibility with WooCommerce Waitlist extension.
* Tweak - Check for `form.cart` before calling Waypoint.

= 1.1.6 - 15.06.2017 =
* Tweak - WooCommerce 2.6/2.7 compatibility.

= 1.1.5 - 10.06.2017 =
* Tweak - WooCommerce 2.7 compatibility.

= 1.1.4 - 10.06.2016 =
* Tweak - Hide the sticky add to cart component on mobile as it takes up too much screen real estate.

= 1.1.3 - 04.26.2016 =
* Tweak - Integration with Catalog Visibility Options extension.

= 1.1.2 - 04.13.2016 =
* Tweak - Compatibility with products other than simple/variable (eg. Subscriptions).

= 1.1.1 - 03.08.2016 =
* Tweak - Storefront 2.0.0 compatibility.
* Tweak - General code tidy up.

= 1.1.0 - 11.06.2015 =
* New - Now displays the product rating as well. Kudos @BurlesonBrad.
* New - Now works for variable products.
* Tweak - Button now uses the `.alt` class to stand out more.
* Tweak - Minor style adjustments.

= 1.0.0 - 10.30.2015 =
Initial release.