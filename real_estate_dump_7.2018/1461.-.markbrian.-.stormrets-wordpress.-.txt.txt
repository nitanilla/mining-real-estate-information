=== Plugin Name ===
Contributors: agentstorm
Donate link: http://www.stormrets.com/
Tags: idx, real estate, realestate, rets, agent, broker, property
Requires at least: 2.9
Tested up to: 3.3
Stable tag: 1.1.35

This plugin integrates StormRETS IDX Functionality into your Wordpress powered blog.

== Description ==

~Current Version:1.2.12~

NOTE: The default templates where changed between 1.1.x and 1.2.x if you do not wish to use the new templates copy agentstorm_result.php from the plugin directory into your theme directory before updating.

Our continually developed Wordpress plug-in is released under the GNUv3 license and contains both Contact Manager and IDX functionality.

The Contact Manager allows you to collect leads from your wordpress blog and automatically save them in your agent storm account. Assign tags to the leads collected and receive notifications immediately when they are received.

Display IDX listings directly on your Wordpress blog which are SEO optimized. Our fully customizable IDX Wordpress plug-in gives you full control how your listings are displayed on your web site. The plug-in places your properties directly on your web site, there are no IFrames and no hidden containers, the information displayed is fully indexable by search engines.

Head over to http://www.stormrets.com/ to find out more about IDX products by StormRETS.

Don't forget to follow us on Twitter @stormretsapp to stay up to date on the latest news and advancements.

Features Include:

* SEO Optimized URL's
* IDX Search Functionality
* Contact Form
* Full Property Information and Property Features
* Google Map of Property (Uses new Google Maps V3 API)
* Bing Maps Birds Eye View
* School Information (If provided by MLS/REALTOR)


== Installation ==

1. Upload the `agent-storm` folder to the `/wp-content/plugins/` directory
1. Activate the plugin through the 'Plugins' menu in WordPress
1. Configure the Plugin via the Administration console

== Frequently Asked Questions ==

= Can I customize the results? =
Yes, See our Support site on how to customize both the stylesheet of this plugin and result page design


== Screenshots ==

1. Results
2. Administration Screen

== Changelog ==

= 1.2.x =

* Added Experimental SYSV Messaging Server for speeding up API requests via HTTP Keepalives
* Default Template Refresh
* Default template is now optimized for load speed several large objects are delay loaded on page scroll to cut the initial page load time
* get_option optimizations using AgentStormSettingCache class
* Fixed bug caused by certain themes wp_foot implementation causing a single request to result in 2 api fetches
* Use AgentStorm Map Library wherever a map is displayed
* Added Additional Display Field section for the property listing page
* Sort Display Fields Alphabetically

= 1.1.x =

* Fixed Admin selectors for available search fields some some browsers
* Fixed error where map would fail to be drawn if property in result is not geocoded
* Map Search Functionality
* Fix issue with Thesis Theme
* Fix returned Status code error
* Added Search Filter Widgets
* Added Request a showing button
* Allow map shortcode to specify lat, lng, zoom, height and width
* Allow overiding the default stormrets templates with templates stored in TEMPATEPATH
* Fix for installing default templates into template dir
* Added 'Saved Properties' and 'Saved Searches' count to the Wordpress User List
* Added list of Saved Properties and Searches to the User Profile Screen.
* Added ability for a user to clear his Saved Properties and Searches
* Added require_login classes to button and search form widgets if force login is true
* Fix tab indexes on register/login lightbox
* Add ability to specify the MLS Number (%listing_id%) on the Property URL Permalink without the %id%.
* Prevent automatic Wordpress redirection for links ending in .html causing a double tap to the API.

= 1.0.x =

* Initial Release
* Removed dependancy on a certain url to find styles and javascript files
* Added Google Map
* Added Bing Birds Eye View
* Added Full Property Information
* Added Property Type Fields to search
* Fixed Problem in 1.0.5 where GMaps javascript would not be included unless the default style checkbox was set
* Added Saving Contacts to Agent Storm system
* Added Source Textbox to define Lead Source in Agent Storm System
* Fixed 404 status being returned for dynamically generated pages
* Fixed Browse Sidebar where would not always be formatted with correct indentation fir cities.
* Added Short codes
* Fixed error caused by a slight API update
* Fixed casing error causing properties to not be displayed
* Added Search by MLS Number Widget
* Added Virtual Tour Button
* Added Agent Information Box
* Added Search Results shown on map
* Added different color themes
* Fixed bug where extra P tags are inserted by Wordpress
* Added ability to expand and contact map
* Added shortcode for Latest Properties added to MLS
* Fixed a bug where the Example API Key and Hostname where not getting populated on activation
* Expanded Short codes to allow complex saved searches for including on pages
* Added enabling and disabling of certain searchable property classes
* New interface to select which fields are displayed on the results list and results page for each respective property type
* Fixed bug in Breadcrumb where the custom prefix was not obeyed
* Fixed bug where unlimited properties would be returned for a query if limit in admin is not set
* Fixed a second bug in the Breadcrumb
* Fixed a bug in paging from the short codes
* Added Short Sale and Foreclosure search options
* Added Checkboxes for enabling the various search fields
* Added Short Sale and Foreclosure to Short Codes
* Added WaterfrontLocation search options to the short codes
* Added configurable permalinks for IDX URL's
* Fixed capitalization State abbreviations
* Added target="_blank" to Virtual Tour Link
* Removed various meta tags added by wordpress which could confuse spiders
* Added correct canonical URL to property posts.
* Fixed missing </span> tags causing an issue with unreadable text in Internet Explorer
* Added ability to select custom template pages for displaying IDX pages
* Fixed an error where certain themes where displaying "Nothing found for" as the page title
* Added detection of All In One SEO Pack and check the config to ensure it is configured correctly for use with Agent Storm
* Added notification of Successful save and redirect to correct tab after save
* Preparations for Internationalization
* Basic obfuscation of agents email address displayed on listing
* Added ability to change default field names on listing pages
* Button to install default templates to assist customization of results pages
* Fixed a bug in the Permalinks causing an issue with sluggified state and cities with spaces
* UI Updates
* Added Sub Division search option
* Added Logged In User Widget
* Searches and Properties can now be saved by Logged In Users
* Added Area Short code

== Upgrade Notice ==

= 1.0 =
None
