=== Google Places Reviews ===
Contributors: wordimpress, dlocc, webdevmattcrom
Donate link: http://wordimpress.com/
Tags: google, reviews, google reviews, google places, google places reviews, google review widget, google business reviews, google review, review, google place review
Requires at least: 3.8
Tested up to: 4.2.1
Stable tag: 1.2.1
License: GPL2

Display Google Places Reviews on your WordPress website and help boost consumer confidence and search engine optimization.

== Description ==

Easily display Google Reviews on your WordPress website using a powerful and intuitive widget. Great for restaurants, retail stores, franchisees, real estate firms, hotels and hospitality, and nearly any business with a website and reviews on Google.

[youtube https://www.youtube.com/watch?v=fXQA5kXRm88]

**[View the Online Demo](http://googleplacesreviews.wordimpress.com/ "View the Online Demo of Google Places Reviews Pro")**

= Why Use this Plugin? =

This plugin allows you to display Google reviews on your WordPress website. Why is this important? Positive reviews on websites like Google help businesses gain additional exposure and further enhance their online credibility. A [recent study](http://marketingland.com/survey-customers-more-frustrated-by-how-long-it-takes-to-resolve-a-customer-service-issue-than-the-resolution-38756) conducted by Dimensional Research found that the buying decisions of 90% of consumers are influenced by positive online reviews. Additionally, a [2012 study published on Search Engine Land](http://searchengineland.com/study-72-of-consumers-trust-online-reviews-as-much-as-personal-recommendations-114152 "View the Article Online") found that 72% of consumers trust online reviews as much as personal recommendations. If you do the research it quickly becomes clear. Positive reviews add substantial credibility to any business and can lead to increased conversion rates and higher sales.

There is significant data that shows how much consumers care about online reviews but very little information about what businesses are doing to respond to this phenomenon. How about displaying reviews on your WordPress website from Google?

Google Places Reviews allows you to display up to 3 business reviews with the free version and 5 with the Pro version. Setup is quick and easy. Simply install the plugin, insert your Google API (free and documented), and drag the widget into any sidebar to configure the options.

= Google Places Reviews Pro =

[Upgrade to Google Places Reviews Pro](http://wordimpress.com/plugins/google-places-reviews-pro/ "Upgrade to Google Places Reviews Pro").

Use Promo Code: `googleplaces20off` for a 20% discount!

= Plugin Features =

* Google Business Reviews - Display up to 3 business reviews per location.
* Detailed Business Information - Show the business name, website, Google+ page and more.
* Versatile Widget Themes - Choose from a selection of stunning widget themes that fit light and dark color schemes that make integration with your website design effortless.
* Google Places Autocomplete - Easily lookup businesses in your area through the widget interface using the power of Google search.
* Actively Supported and Developed - We are a team of expert developers based in San Diego, California and we stand by our work. Got a problem? Hit us up.

= Google Places Reviews Pro Version Features =

Google Places Reviews Pro is a significant upgrade to Google Places Reviews that adds many features to the core plugin:

* More Reviews - Display up to 5 reviews using the Google Places API
* Powerful Shortcode - Display reviews in your post and page content
* Review concatenation - Some reviews returned by Google may be very long which could result in a very long widget. The Pro version includes a customizable feature for collapsing and expanding long reviews with "Read more" and "Close" links.
* Fast loading - Optimized widget caching included within the plugin ensure you save on load time and API calls
* Priority Support - Get fast and responsive support from WordPress experts in the USA for the lifetime of your license.

= Additional Business Reviews Plugins =

Why limit your reviews to just Google Places Reviews? Check out our other free business reviews plugins to add to your site as well:

* [Yelp Widget Pro](https://wordpress.org/plugins/yelp-widget-pro "Yelp Widget Pro")
* [Yellow Pages Reviews](https://wordpress.org/plugins/yellow-pages-reviews/ "Google Places Reviews")
* Get all three of our Premium Business Reviews plugins for one low price. [Premium Business Reviews Bundle](https://wordimpress.com/plugins/business-reviews-bundle/?utm_source=WordPress.org&utm_medium=readme&utm_campaign=Yellow%20Pages%20Repo "Premium Business Reviews Bundle")

== Installation ==

1. Upload the `google-places-reviews` folder and it's contents to the `/wp-content/plugins/` directory or install via the WP plugins panel in your WordPress admin dashboard
2. Activate the plugin through the 'Plugins' menu in WordPress
3. That's it! You should now be able to use the widget.

Note: If you have WordPress 2.7 or above (and I hope you are) you can simply go to 'Plugins' > 'Add New' in the WordPress admin and search for "Google Places Reviews" and install it from there.

== Frequently Asked Questions ==

= Why does the widget look funny in my theme? =

Most likely your theme has conflicting CSS that is interfering with the themes included with the plugin. If you're handy with CSS this can be an easy fix. If you are new to CSS then try out the Bare Bones theme to see if that looks nicer. Otherwise, you may have to hit up your coding friends to help you out.

= Are style (CSS) and/or theme compatibility issues supported? =

We do our best to support the free version of the plugin but it's not our priority. The premium plugin is where we spend most of our support time. If you are experiencing a style issue and need help, either upgrade to the Premium version or post in the WordPress.org support forum and we will do our darnedest to get it set up nicely for your theme.

= Are there prebuilt styles included in the plugin? =

Yes, there are three basic themes included in the free version of the plugin. The premium version has many more options and themes.

== Screenshots ==

1. An admin view of the widget in a WordPress sidebar

2. Minimal widget themes displayed on the demo site

3. Shadow widget themes displayed on the demo site

4. Inset widget themes displayed on the demo site

5. The plugins settings page found under Settings > Google Reviews

== Changelog ==

= 1.2.1 =
* Fix: Broken avatar images displayed for some reviews where the user had not set an avatar

= 1.2 =
* New: Language .pot file for translators
* New: Added additional widget field tooltips
* New: Place "Type" filter to help users find their locations' Place ID on Google
* Update: Switched from Google Places API "Reference" to "Place ID"
* Update: Textdomain changed from 'google-places-reviews' to a much more manageable 'gpr'
* Update: Better tooltip output using new gpr_admin_tooltip function
* Update: Removed usage of GPR_DEBUG in favor of SCRIPT_DEBUG constant
* Fix: "Clear Cache" button under Advanced Options now actually clears the cache
* Fix: Several minor PHP warnings and notices
* Fix: UX improvement: "Hide Google Logo" label wasn't click-able to select checkbox, now it is
* Fix: Minor admin CSS touch ups for WP 4.2

= 1.1.3 =
* Modified text in activation banners so it's more informative & relevant to the free version

= 1.1.2 =
* Added activation banner
* Updated readme.txt
* Fully I18n (internationalization) ready

= 1.1.1 =
* Fix: "Disable Title Output" under the "Advanced Options" in the widget wasn't working, it is now; thanks "game writer" for notifying us of this bug.
* Fix: Avatar image overlapping into the content because of lack of max-width CSS property.

= 1.1.0 =
* New: Plugin thumbnail that now appears in WP repo search
* Improvement: If an error occurs the widget will output them and then ensure that the bad result is not cached so if the user fixes the error they won't have to manually clear the cache.
* Minor improvements the the widget's frontend appearance
* Fixed bad links to plugin docs
* Tested WP 4.0 functionality to approve bumping version compatibility

= 1.0.1 =
* Update: Removed schema.org tags from the free version of the plugin.
* Update: Fixed minor CSS issues with star counts collapsing below review avatar for some sidebars with tight widths; several padding reductions to support slimmer widths.

= 1.0 =
* Initial Free version release!