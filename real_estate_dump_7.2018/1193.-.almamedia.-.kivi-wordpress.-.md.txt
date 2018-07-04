# KIVI WP-plugin
- Requires at least: 4.0
- Tested up to: 4.9.4
- Stable tag: 1.0.8
- License: GPLv2 or later (http://www.gnu.org/licenses/gpl-2.0.html)

- *PHP >= 5.5.0 required*, 5.5.9 tested
- php GD support required
- php DOM required (http://php.net/manual/en/book.dom.php)
- php settings:
	-	”allow_url_fopen” On
	-	”memory limit” at least 128M
	-	”max_execution_time” at least 30
- enough memory on server to create image thumbnails (2GB+)
- no BasicAuth ( blocks async request )


## Description

A plugin for displaying KIVI real estate system properties on a WordPress site. The plugin is not meant to be out-of-the box solution
for the job, but instead a starting point for development. With the plugin, simple index and single templates are provided for listing and displaying the properties.

KIVI Wordpress plugin imports KIVI data into Wordpress as a background process. The plugin is scheduled to read the active items in the KIVI system every hour. New items are added, deleted items are deleted and updated items are updated. In WordPress, the KIVI items are stored ad a custom post type named `kivi_item`. Item images are stored in the WordPress media gallery and referenced in the kivi_item posts. Kivi_item posts are not supposed to be edited using the WordPress editor as the scheduled update from the KIVI system will overwrite any changes if the item is changed in KIVI.

For getting the correct export from KIVI system, a specific WordPress transfer needs to be opened first. For more information, contact the sales or the customer support kivi@almamedia.fi.

## Installation

Just drop extract the package in the `plugins` directory of your WP installation. 'KIVI items' and 'KIVI' tabs will appear in the dashboard. 'KIVI' is the admin area, 'KIVI items' will list the imported items.

## Settings

- XML address for importing. This you will get from the KIVI customer service. This is customer specific and will include all the items for a specific customer.

- Brand color. This will change some the colors of the plugin provided template page. For real customisations and theme like look and feel, a separate template for KIVI items should be implemented on the template directory.

- Slug. Define a slug for the kivi_item post type. This is basically a piece of the url structure for your KIVI-items. For example in item url http://www.example.com/kohde/5hks-tampere-jokupolku-4/ the 'kohde' would be the slug. Also the list of all the items can be accessed using the url `<site url>/<slug>`.

- Show sidebar on item page. This controls if the default item template will call `get_sidebar()` or not.

- 'Use www sized images in transfer (default: original)' Use www-size images when transferring the items to WP. Www-sized are smaller than originals. This is useful for in development phase as the www images download quicker. Using originals in production is a good idea.

- Clean values. Alters property data to look better. Replaces "m2" with "m²", addds euro sign to prices and formats numbers. For additional formatting, use the filter "kivi_viewable_value" ( with up to three attributes: value, label, properties).

- Google maps api key. If set, a google maps component is shown on the item page and the property is pinned on the map. The location is based on the address and geocoded using google's api. Note that there is a limit of geocoding requests for a single api key.

- Reset. This will reset the settings and remove all KIVI items.
- Save settings. This will (obviously) save the settings.

## Adapting to a theme

The plugin has default templates for listing properties and displaying a single item. The templates might work with your theme just fine, or not. You can place your own templates in your theme's directory and these will override the ones defined by the plugin. The files sould be `kivi-index-template.php` and `kivi-single-template.php` for index page and single item page, respectively. You can of course use the default templates as a starting point for your own templates, the files are  `includes/partials/kivi-index-template.php` and `includes/partials/kivi-single-template.php`.

## Shortcodes defined by the plugin

You can use shortcodes to display KIVI data in your own custom WordPress pages by adding a shortcode defined by the plugin in the content of the page.

### List items by town
`[kunta nimi='<city>']`

for example:
`[kunta nimi='Tampere']`

### List items by housing company
`[taloyhtio nimi='<housing company name>']`

for example:
`[taloyhtio nimi='Asunto Oy Tampereen Pohtola']`

### List items by item type
`[tyyppi nimi=<item type name>]`

for example:
`[tyyppi nimi="omakotitalo"]`
or
`[tyyppi nimi="omakotitalo" toimeksianto="vuokra"]`


### List items by item group
`[tuoteryhma nimi=<item group name>]`

for example:
`[tuoteryhma nimi="toimitilat"]`

Possible item groups are: asunnot,loma-asunnot,toimitilat,tontit,vuokra-asunnot,loma-asunnot,uudiskohteet, "maa- ja metsätilat", "autotallit ja muut"

### List items by assignment type
`[toimeksianto tyyppi=<assignment type>]`

for example:
`[toimeksianto tyyppi="vuokra"]`
or
`[toimeksianto tyyppi="myynti"]`


## Feature Requests and Contributing

We are not too actively developing individual features for the plugin as it's meant to be a starting point for development anyways. However, we do fix bugs and for example add support for new data if such data appears in the source system. If there are specific needs you can of course contact our sales.

We are also happy to accept any pull requests if they are generic enough and seem fit for our users.

## Changelog

**1.0.9**
- Minor refactor

**1.0.8**
- Make unique id selections more strict and fix code to work more as expected
- Add missing property information
- Fix pagination on default index template

**1.0.7**
- Added video/3d links
- Better dublicate handling
- show next sync time or sync-off notice in admin view

**1.0.6**
- Better handling for a situation when there are no items to display.

**1.0.5**
- Changed default item order in listing. (merged branch list-order)
- Fixed data update to work like it is specified in readme. All item data, including post_content and post_title, will now update from Kivi.

**1.0.4**
- Added possibility for prefiltering items while importing

**1.0.3**
- Missing assets of slick carousel (Issue #3)
- More specific css selectors for admin css (Issue #2)
- Shortcode for listing based on assignment type (PR #1)

**1.0.2**
- Added shortcode for listing items based on item type. Patch submitted by @karikauppinen

**1.0.1**
- Fix scheduling initalialization (the scheduling did not work at all)
- Change scheduling interval to 15 minutes

**1.0.0**
- Initial version
