# Shift8 Treb IDX Wordpress Plugin
* Contributors: shift8
* Donate link: https://www.shift8web.ca
* Tags: treb, toronto real estate board, toronto real estate, wordpress, treb wordpress, wp, toronto wordpress
* Requires at least: 3.0.1
* Tested up to: 4.5.2
* Stable tag: 0.5
* License: GPLv3
* License URI: http://www.gnu.org/licenses/gpl-3.0.html

Wordpress plugin that easily integrates and imports your TREB (Toronto Real Estate Board) data.

# Important Notice

This plugin is still under very active development. It is not considered stable by any means. Feel free to watch and/or reach out directly to get more information.

## Description 

This is a small plugin that allows you to import your TREB listing data into Wordpress easily and seamlessly. Most importantly, this plugin requires no 3rd party service and no monthly service fee. The plugin assumes you already have taken the necessary steps to gain access from TREB for FTP and Web access to the data. You must have a TREB Agent ID, TREB Username and TREB password to use this plugin. 

Future versions of this plugin will allow cron scheduling and automated import processes. Note this plugin is using an asynchronous non-blocking queuing system to process the data and listing images. This is because the connection to TREB's systems is notoriously slow and can cause timeouts on many hosting environments (or even dedicated server environments). The queueing system offloads those lengthly processes in such a way to avoid breaking the data process. 

TREB's FTP service is very slow so the import process for 20 listings can take up to 10 minutes to complete.

## Installation 

This section describes how to install the plugin and get it working.

e.g.

1. Upload the plugin files to the `/wp-content/plugins/shif8-treb` directory, or install the plugin through the WordPress plugins screen directly.
2. Activate the plugin through the 'Plugins' screen in WordPress
3. Navigate to the plugin settings page and define your TREB Agent ID, TREB Username and TREB Password
4. Pressing the "Import" button will import listings. Please watch the progress bar for the completion status. Once complete the plugin will import Wordpress posts with the data


## Frequently Asked Questions 

### How can I schedule this to be automatic?

This plugin is still very new and this is planned for a future version.

### Can I import data from a specific date?

This will be an option for a future version

### What else have you done?

You can visit [our website](https://www.shift8web.ca "Toronto Web Design") to see! :)

### Screenshots 

1. There are currently no screenshots

## Changelog 

### 0.5
* Beta version created
* Implemented queuing system

