=== Altos Widgets ===

Version: 1.3.2
Stable tag: trunk
Tested up to: 4.1
Requires at least: 2.8.4
Plugin Name: Altos Widgets

Author: AltosResearch.com
Contributors: AltosResearch
Author URI: http://www.altosresearch.com/
License: http://www.gnu.org/licenses/gpl-2.0.txt
Plugin URI: http://www.altosresearch.com/wordpress-plugins
Tags: widget, widgets, altos, altos research, altosresearch, real estate, property, charts, graphs
Description: Easily embed tables and charts of current Altos Research real estate statistics on your website.

Easily embed tables and charts of current Altos Research real estate statistics on your website.

== Installation ==

1. Upload the `/altos-widgets` folder to your `/wp-content/plugins/` directory.
2. Activate the plugin through the `Plugins` menu in WordPress®.
3. Navigate to `Appearance->Widgets` and add the widgets.

== Description ==

Easily embed tables and charts of current Altos Research real estate statistics on your website.

== Screenshots ==

1. Altos Widgets / Screenshot #1
1. Altos Widgets / Screenshot #2
1. Altos Widgets / Screenshot #3
2. Altos Widgets / Screenshot #4

== Upgrade Notice ==

= 1.3.2 =
* Bug fix in update stat table widgets

= 1.3.1 =
* Bug fix in stat table title

= 1.3.0 =
* Updated icons and confirmed working with 3.6

= 1.2.7 =
* Updated login features

= 1.2.5 = 
* Updated to see if it shows up in the search feature again

= 1.2.4 =
* After upgrading, you'll need to re-insert any existing widgets that you've been using. In other words, after upgrading, all existing Altos Widgets that you currently have in your Sidebar, will automatically disappear, and you'll need to re-insert updated versions of each widget.

== Changelog ==

= 1.2.4 =
* Updated to support the `WP_Widget()` class, in WordPress® 2.8.4+. This provides multi-widget capabilities.
* Updated to support multi-widget Chart locations; and also transition effects for multi-widget Chart locations.
* Updated requirements to WordPress® 2.8.4+. Altos Widgets are no longer compatible with back-dated versions of WordPress®.

= 1.2.2 =
* Added support for WordPress® 3.0 `wp_loaded`.
* Fully tested in WordPress® 3.0, including with `MULTISITE` ( i.e. networking ) enabled. Everything looks good.
* Added support for 2-year/3-year chart timespans.

= 1.2.1 =
* Bug fixed in `validate_pai()` method. This function now returns null on failure.
* Support for both `file_get_contents()`, and a fallback on cURL has been established through a new method, `fetch_url_contents()`. This makes the plugin compatible with GoDaddy, Dreamhost, and other hosts that disable `allow_url_fopen` by default.
* A new administrative notice is displayed on the Plugins Panel whenever `pai` authentication is non-existent or invalid.

= 1.2 =
* Initial release on WordPress.org.
