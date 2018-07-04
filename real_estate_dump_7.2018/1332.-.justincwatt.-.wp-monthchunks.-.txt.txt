=== Monthchunks ===
Contributors: justincwatt, xavivars
Donate link: http://justinsomnia.org/2005/04/monthchunks-howto/
Tags: archive, archives, template tag, wp_get_archives, sidebar
Requires at least: 3.0
Tested up to: 4.7
Stable tag: trunk
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Concisely display monthly archives by year with links to each month.

== Description ==

Display monthly archives by year with links to each month in the following compact format:

    2012
    1 2 3 4 5 6 7 8 9
    
    2011
    1 2 3 4 5 6 7 8 9 10 11 12
    
    2010
    6 7 8 9 10 11 12

Serves as a drop in replacement for [`wp_get_archives( array( 'type' => 'monthly' ) );`](http://codex.wordpress.org/Function_Reference/wp_get_archives).

If you're interested in contributing to the code behind this plugin, it's also hosted on GitHub:
https://github.com/justincwatt/wp-monthchunks

== Installation ==

1. Extract the zip file, drop the contents in your wp-content/plugins/ directory, and then activate from the Plugins page.
1. Edit your theme file (e.g. sidebar.php) and replace the WordPress template tag `wp_get_archives();` with `monthchunks();`
1. You can also add it as a widget to any sidebar

== Frequently Asked Questions ==

= How do I make the years display in ascending order (2010, 2011, 2012...) instead of descending (the default)? =

The monthchunks function takes two optional parameters and the first is `year_order`, which accepts two string values: `"descending"` or `"ascending"`.

= Can I make months display in a format other than the default month number (1, 2, 3...)?

The monthchunks function takes two optional parameters and the second is `month_format`, which accepts three string values: `"numeric"`, `"alpha"`, or `"abbreviation"`. The "alpha" format displays the first letter of the month (e.g. J, F, M...) which may not make sense in all languages. The "abbreviation" format displays the language-specific abbreviation for the month, e.g. (Jan, Feb, Mar...).

== Screenshots ==

1. This is how Monthchunks looks with the Twenty Eleven theme. You can see here that 4 years of archives (eventually 48 links) take up less than 200 vertical pixels of precious sidebar real estate. Note that if you're browsing a monthly archive page, that month's number is emboldened, but not linked. If you hover over the link for any month, you'll see the localized month name and year as a *tooltip*.

== Changelog ==

= 3.1 =
* Changed l10n to adjust to new plugin translation process
** Updated text-domain

= 3.0.4 =
* Fix PHP Notice, incorrectly using variable instead of instance field. (thanks Birgir Erlendsson - @birgire)

= 3.0.3 =
* Improve class constructor

= 3.0.2 =
* Fix backwards compatibility calls to monthchunks

= 3.0.1 =
* Fix admin area issue

= 3.0 = 
* Major refactor of the code
** Created different files to split the backend logic and the widget
* Includes widget support
* Added localization templates

= 2.4 =
* Added the new "abbreviation" mode for month display (thanks Xavi Ivars)

= 2.3 =
* Use WordPress' Date and Time Locale object to localize month names in tooltip
* Change default year_order sort to descending (more closely matches wp_get_archives)
* Appropriately escape html output (though largely unnecessary)
* Fix: only display archive link for months with posts (not pages)

= 2.2 =
* Generate output with a single SQL query, instead of N+1, where N was the number of years of post archives

= 2.1 =
* Add year_order and month_format options
* Add `title="month_name year"` attribute (aka tooltips) to the month links 
* Lmited visible archives to posts with post_status = 'publish'
* Revise pretty html output slightly
* Add semifix for year = "0000" bug

= 2.0 =
* Remove `<ul></ul>` output to make monthchunks more of a drop-in replacement for `wp_get_archives()`
* Add logic to de-link from current month
* Sort years in chronlogical order
* Don't print separator space after last month of year

= 1.2 =
* Use `$wpdb->posts` instead of `wp_posts` as table name

= 1.1 =
* Use WordPress' `get_month_link()` function to output link to monthly archive (thanks raphaële)

= 1.0 =
* Initial version

== Upgrade Notice ==
= 2.2 =
Improved performance of SQL queries

= 2.0 =
Monthchunks is now a drop-in replacement for `wp_get_archives()`

= 1.0 =
Initial version
