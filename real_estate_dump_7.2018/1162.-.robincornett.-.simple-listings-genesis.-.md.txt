# Simple Listings for Genesis

WordPress plugin that adds a custom post type and taxonomy for real estate listings.

## Description

This plugin registers a simple custom post type for real estate listings. It also registers a separate listing taxonomy. The plugin supports a featured image, general description, MLS link, location, and price. It does not support detailed input such as square footage, number of bedrooms, etc. If you need that, use [AgentPress Listings](http://wordpress.org/plugins/agentpress-listings/) instead.

If your site is running a Genesis Framework child theme, this plugin includes a template for the archive, taxonomy, and single listing page. If you're not running the Genesis Framework, you can create your own templates for these in your theme. You can also override these with your own templates/styles in your theme.

*Note: although this plugin was written with the [Genesis Framework by StudioPress](http://studiopress.com/) in mind, it is not an official plugin for this framework and is neither endorsed nor supported by StudioPress.*

Demo: http://robin.works/listings/

## Requirements
* WordPress 3.8, tested up to 4.9
* Genesis Framework (templates and widget will not work with other themes, although post type and metaboxes will work with any theme)

## Installation

### Upload

1. Download the latest tagged archive (choose the "zip" option).
2. Go to the __Plugins -> Add New__ screen and click the __Upload__ tab.
3. Upload the zipped archive directly.
4. Go to the Plugins screen and click __Activate__.

### Manual

1. Download the latest tagged archive (choose the "zip" option).
2. Unzip the archive.
3. Copy the folder to your `/wp-content/plugins/` directory.
4. Go to the Plugins screen and click __Activate__.

Check out the Codex for more information about [installing plugins manually](http://codex.wordpress.org/Managing_Plugins#Manual_Plugin_Installation).

### Git

Using git, browse to your `/wp-content/plugins/` directory and clone this repository:

`git clone git@github.com:robincornett/simple-listings-genesis.git`

Then go to your Plugins screen and click __Activate__.

## Frequently Asked Questions

### How can I display listing items differently than regular posts?

If you're using a Genesis Framework theme, it's done. If you're not, use the included templates as a reference and have fun.

### Why did you make this?

The AgentPress Listings plugin has a lot more features and functionality than I needed for a couple of projects, so I thought I'd make a simple version which would allow my client to post their own listings on their own site, but optionally link to the outside MLS service listing. They can feature their own listings without having to re-enter all of the data.

### How do I start?

Simple Listings for Genesis works much like creating any other post or page in WordPress. One important thing is that when you are creating a listing, you must set a featured image. If you don't, there is a fallback image, but I'm pretty sure you would rather use your own. Everything else is more or less optional--whether you want to use a description, an outside MLS link, transaction amount, or location.


## Screenshots ##
![Admin: show all listings.](https://github.com/robincornett/simple-listings-genesis/blob/master/assets/screenshot-1.png)  
__Screenshot of all listings in Admin.__

![Admin: create/update a new listing. Note metaboxes and featured image.](https://github.com/robincornett/simple-listings-genesis/blob/master/assets/screenshot-2.png)  
__Admin: create/update a new listing. Note metaboxes and featured image.__

## Changelog

### 1.6.2
* Updated stable version, WordPress tested version

### 1.6.1
* Fixed widget to correctly accept term selection.

### 1.6.0
* Revised single listing output--now uses the_content filter.

### 1.5.0
* Removed CMB2 from plugin files, since it's now on the repository. Use TGMPA to require CMB2
* Refactored everything, cleaned up template files

### 1.4.1
* bugfix: invalid header warnings on activation (CMB2)

### 1.4.0
* added admin columns
* updated single-listing
* updated custom metaboxes (CMB2)
* compatible with WP4.1

### 1.3.0
* added XHTML actions/styling for backwards compatibility.
* removed irrelevant image alignment option from widget.
* CSS tweaks.

### 1.2.1
* Translation strings corrected
* Single listing template cleaned up (primarily for translation)
* Fallback image added/set for archive template and widget, if no featured image is set in listing. You really should set a featured image.
* CSS corrected so archive listing-wrap doesn't have a background
* Added xml folder/import file so you could import sample listings

### 1.2.0
* Reorganized file structure
* Reconfigured how templates are loaded
* Body class function for archive/taxonomy moved to template file

## Credits

Built by [Robin Cornett](http://www.robincornett.com/)
