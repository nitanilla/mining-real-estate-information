wp-realestate-sync
==================

The easiest way to publish properties on your wordpress site, direct from your real estate software.

## Description

WP-realestate-sync is a Wordpress plugin which allow you to synchronize your real estate Wordpress site with Gedeon API http://api.gedeon.im/doc.

Currently supported themes are :
* WPCasa based (http://wpcasa.com)
* Realto (http://themeforest.net/item/realto-wordpress-theme-for-real-estate-companies/6801549)
* Decorum (http://themeshift.com/theme/decorum/)

more are coming soon !


## Installation

1. Unzip plugin to the `/wp-content/plugins/` directory
1. Or, install it through Wordpress plugin repo.
1. Activate the plugin through the 'Plugins' menu in WordPress
1. Set your API key in Settings->Realestate Sync menu (don't have one ? Contact us at api@gedeon.im to get one)

## Frequently Asked Questions

### The theme I use is not supported, what can I do ?

Let us know at wordpress@lsi.im that you are interrested by this particular theme, We will develop a connector as soon as possible, after validate that it's possible for this theme.

If your an adventurer, you can develop yourself the compatibility by forking theis repo.

### I'm a theme creator, I want to be compatible with your plugin, what can I do?

1. Take a look to understand how plugin work
1. Fork the project and develop your own connector.
1. Or, if your are not a developer, let us know at wordpress@lsi.im that you would be compatible. 

### But, is it a realtime connection with your API ?

No. Most of the real estate themes stores properties in custom posts. The plugin just create custom post in wordpress by following theme rules.

A cron import properties at chosen rythm (hourly, daily, ...).

### Okay, but it's only synchronises properties

No, for example it adds a DPE (french-specific energy consumption indicator) Widget to WPCasa based themes. Others features like that are planned.




