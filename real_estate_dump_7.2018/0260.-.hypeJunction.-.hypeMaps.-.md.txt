hypeMaps
========
![Elgg 1.10](https://img.shields.io/badge/Elgg-1.10.x-orange.svg?style=flat-square)
![Elgg 1.11](https://img.shields.io/badge/Elgg-1.11.x-orange.svg?style=flat-square)
![Elgg 1.12](https://img.shields.io/badge/Elgg-1.12.x-orange.svg?style=flat-square)
![Elgg 2.0](https://img.shields.io/badge/Elgg-2.0.x-orange.svg?style=flat-square)

Google Maps integration for Elgg


## Support the development

1. [Buy me a vegetable!](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=P7QA9CFMENBKA)
2. You can also support the development of this plugin by sharing a percentage of
your real-estate allocated to AdSense Units. You can specify the percentage you
would like to share with me (0 to 100) in the plugin settings.
On every page load, the plugin will switch between your publisher ID and
my publisher ID. E.g. if you choose to share 10%, your publisher ID will be used
on 90% of all page views, my publisher ID will be used on 10% of page views

## Getting Started

* You will require a valid Google API key. You can obtain one at
https://console.developers.google.com.
Configure your project to include the following APIs:
* Static Maps API
* Google Maps Javascript API
* Google Maps Geolocation API
* Geocoding API

* Geocoding features are not included with this plugin. You will need to install
another plugin fit for that purpose. You can use my hypeGeo plugin found here:
https://github.com/hypeJunction/hypeGeo

* Places features have been decoupled into a separate plugin, so grab a copy of that
if you are upgrading from previous versions:
https://github.com/hypeJunction/hypePlaces

* Make sure you restrict the use of your API Key to domains you administer, otherwise
someone else can copy them from public facing JS/static map URLs and reuse them


## Developer Notes

* Similar to how the gallery view is toggled, map view can be toggled by adding
```?list_type=mapbox``` to any page that has a list generated using core API

* To build and show a new dynamic map, use something along these lines:

```
// Display friends on the map
$params = array(
	'options' => array(
		'id' => 'friends', // List id / must be unique on the page
		'types' => 'user',
		'relationship' => 'friend',
		'relationship_guid' => elgg_get_logged_in_user_guid()
	),
	'getter' => 'elgg_get_entities_from_relationship',
);
echo \hypeJunction\Maps\ElggMap::showMap($params);
```
This example will render a map of user's friends. The generated map will be
filterable, as appose to the one you would have generated using
```elgg_list_entities_from_relationship()``` passing ```'list_type' => 'mapbox'```

Note that maps generated in this fashion will only include entities taht have
a geocoded location. If you need a list of all entities with an additional map
overview, use ```elgg_list_entities_*``` and pass a mapbox list type.


* To modify a list of sitewide or group maps, use ```'search:site','maps'``` and
```'search:group','maps'``` hooks. See the code for some examples.
You will need to add your custom views.


## Screenshots

![alt text](https://raw.github.com/hypeJunction/hypeMaps/master/screenshots/map_users.png "User search")
