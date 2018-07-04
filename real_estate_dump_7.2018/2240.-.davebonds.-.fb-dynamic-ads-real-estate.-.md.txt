# FB Dynamic Ads for Real Estate #
**Contributors:** [davebonds](https://profiles.wordpress.org/davebonds)  
**Author link:** https://davebonds.com  
**Tags:** facebook, facebook ads, dynamic listings, real estate, impress listings  
**Requires at least:** 3.5  
**Tested up to:** 4.9  
**Requires PHP:** 5.6  
**Stable tag:** 1.2.1  
**License:** GPLv2 or later  
**License URI:** http://www.gnu.org/licenses/gpl-2.0.html  

Adds XML feed formatted for FB Dynamic Ads for Real Estate to the IMPress Listings plugin.

## Description ##

**New!** Facebook pixel code is automatically added for you, just enter your pixel ID!
**New!** Pixel events are tracked when a search is performed or listing is viewed.

This plugin adds an XML feed for [IMPress Listings](https://wordpress.org/plugins/wp-listings/) formatted to standards and requirements for [FB Dynamic Ads for Real Estate](https://developers.facebook.com/docs/marketing-api/dynamic-ads-for-real-estate/) Listing Catalogs.

For specific information on setting up real estate listing catalogs, view the [Documentation for Facebook Dynamic Ad Listing Catalogs](https://developers.facebook.com/docs/marketing-api/dynamic-ads-for-real-estate/catalog).

Support for this plugin is handled on [Github](https://github.com/davebonds/fb-dynamic-ads-real-estate). 

## Installation ##

1. In the 'Plugins' menu in WordPress, search for FB Dynamic Ads for Real Estate
2. Activate the plugin through the 'Plugins' menu in WordPress

*Note* The [IMPress Listings](https://wordpress.org/plugins/wp-listings/) plugin is required for this plugin to work.

## Frequently Asked Questions ##

### How do I access the listing catalog XML file? ###

The plugin adds a new feed url at yourdomain.com/feed/fb-catalog/

### How do I have create a listing catalog with more than the default 10 listings? ###

The feed template supports a query parameter of ?numposts=X - where X is the number of listing posts to display.
Example: https://yourdomain.com/feed/fb-catalog?numposts=25

### How do I have create a listing catalog for just one location? ###

The feed template supports a query parameter of ?location=X - where X is the slug of your location taxonomy term.
Example: https://yourdomain.com/feed/fb-catalog?location=my-neighborhood

### My listings already have a Status and Property Type set with a taxonomy, why do I have to select one from the metabox? ###

This is because the fields required by Facebook only accept specific values and cannot reliably be matched to a user-defined value.

### Why are my listings not displaying in the catalog feed ###

This is most likely due to your listings missing one of the required fields. For a list of the required fields, view the [dynamic ad catalog documentation](https://developers.facebook.com/docs/marketing-api/dynamic-ads-for-real-estate/catalog).

### Will this plugin support other real estate listing plugins? ###

Not likely unless there is an overwhelming interest to do so.


## Screenshots ##

1. Listing post metabox for Dynamic Ads fields.

## Changelog ##

### 1.2.1 ###
* Fix: Replaced `get_the_excerpt` description element in feed with trimmed `get_the_content` due to FB parsing issues with HTML entities.
* New: Added `fb_dare_feed_description` filter for feed description element.

### 1.2.0 ###
* New: Adds Facebook pixel code.
* New: Will now output pixel events for viewing a listing (`ViewContent` event) and search for listings (`Search` event).
* New: Also adds standard pixel events for `PageView` and `ViewContent` for other non-listing WordPress content.

### 1.1.0 ###
* New: Added metabox to listing edit screen to select fields formatted for listing catalog feed (availability, property type, listing type).
* New: Added availability, property type, and listing type fields to XML.
* New: Added `neighborhood` field to XML (uses `locations` default taxonomy).
* New: Add settings to input Facebook account identifiers.

### 1.0 ###
* Initial release.


## Roadmap ##

* Determine best way to hook into InitiateCheckout and Purchase events
