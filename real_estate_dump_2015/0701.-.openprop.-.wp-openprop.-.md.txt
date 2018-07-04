# Open Prop

Real estate listings feed import


##Description

_WP Open Prop_ lets you import your existing real estate listing feeds into your WordPress site. Don't just rely on the portals for enquiries and traffic - display your listings on your own WordPress site with your company branding and receive enquiries directly via email form 

## Features

* Import feeds in the most popular listing formats: xx, xx and xx
* .
* Uses [PHPDoc](http://en.wikipedia.org/wiki/PHPDoc) conventions to document the code.
* Example values are given, so you can see what needs to be changed.
* Uses a strict file organization scheme to make sure the assets are easily maintainable.
* Note that this boilerplate includes a `.pot` as a starting translation file.

## Contents

The WordPress Plugin Boilerplate includes the following files:

* This README, a ChangeLog, and a `gitignore` file.
* A subdirectory called `plugin-name`

## Installation

1. Copy the `plugin-name` directory into your `wp-content/plugins` directory
2. Navigate to the *Plugins* dashboard page
3. Locate the menu item that reads *Plugin Name*
4. Click on *Activate*

This will activate the WordPress Plugin Boilerplate. Because the Boilerplate has no real functionality, nothing will be added to WordPress; however, this demonstrates exactly how your plugin should behave while you're working with it.

A new menu item will be added to the *Plugins* menu if you uncomment Line 71 in the class file which contains the following line:

`add_action( 'admin_menu', array( $this, 'add_plugin_admin_menu' ) );`

## License

TODO

## Important Notes

### Licensing

TODO: To be confirmed 
