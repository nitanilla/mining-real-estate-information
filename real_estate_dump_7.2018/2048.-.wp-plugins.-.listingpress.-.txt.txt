=== ListingPress ===
Contributors: jasonbenesch
Donate link: http://listingpress.com/registration
Tags: real estate, listings, seo
Requires at least: 2.8
Tested up to: 2.8
Stable tag: 1.0.5

ListingPress automatically embeds real estate listings on to a wordpress blog.

== Description ==

ListingPress creates a Wordpress-esque query system for a registered real estate agent in the United States to automatically embed listings in to their Wordpress blog. 

The plugin is free and open source (released GPL) but unfortunately the listing data is not. For more information on this, please visit ListingPress.com. 

To install this plugin we recommend creating two more templates; listings.php and listing.php.  The ListingPress loop is almost identical to the Wordpress loop.  We have used the same vernacular and structure as Wordpress does, so that even the casual Wordpress developer will be able to easily implement ListingPress on a real estate agent's blog.  

== Installation ==

1. Upload the entire directory 'listingpress' to the /wp-content/plugins/ directory so it should look like this -> /wp-content/plugins/listingpress
2. Ensure that a cache folder exists and is writable by the server -> /wp-content/plugins/listingpress/cache
3. Activate the plugin through the 'Plugins' menu in the WordPress Administration.
4. Enter your registration code under the ListingPress Settings page.

== Frequently Asked Questions ==

= Why do I need a registration code? =

The way listings work in the United States is like this: 

Similar to stocks, only Real Estate Brokers can buy and sell real estate. Real estate agents are similar to sales agents for their brokers. Every agent has to "hang" their license with a broker. These many brokers across the country get together regionally and form what are called associations. These associations, which again are made up of several large brokers and many little brokers, sign a broker reciprocity agreement. You can advertise my listings as long as I can advertise yours. The associations than hire an outside company to manage the listing data. This outside company creates private web applications that allow real estate agents to upload listings to a central database and search the listings for their clients. For many years, this was the only way anyone could see all the available listings. 

But recently there has been a movement to standardize the industry, referred to as RETS (real estate transaction standard). This standardization is requiring these private companies to provide a uniform way of accessing the data. Then vendors (such as ListingPress) can come in and access that data and provide public facing web applications to display this data. There are fees at every step, as well as a ton of legalities on exactly how you can display this listing data on your website. Therefore, every agent using ListingPress, actually needs to be registered with their specific association so that they may monitor how the listing data is displayed on their site.  While we are actively pushing the envelope on how agents can advertise listings, at this point, it is not a free service and to use this plugin you must be a registered real estate agent. On the positive side, there are a lot of opportunities for developers to make money setting up Wordpress blogs with ListingPress for a real estate agent. If you are interested in learning more, please email me at jason (at) listingpress (dot) com.

= How can I obtain a registration code? =

Visit http://listingpress.com/registration to get a registration code.

== Screenshots ==

1. /screenshot-1.png
2. /screenshot-2.png


== Changelog ==

= 1.0.1 =
* Changed every file to all lowercase letters to be more inline with how WP runs things.

= 1.0.2 =
* Updated lp_query.php -> added an if statement to lp_query->query to prevent the query if the query_string is blank.
* Commented out the lp forms api until it is completely finished.

= 1.0.5 =
* Beefed up the core
* Added Zillow library
* Added Menu Bar
* Added Shortcode
* Added Google XML Sitemap action hook
* Added a featured listing widget

== Some ListingPress Features ==

1. Embeds listings in to wordpress blog for better seo.
2. Pretty permalink urls.
3. Easily embed google maps.
4. 100% customizable.

Many more coming soon.
