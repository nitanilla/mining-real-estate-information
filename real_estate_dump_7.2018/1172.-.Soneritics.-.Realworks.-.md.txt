# Realworks
[![Build Status](https://travis-ci.org/Soneritics/Realworks.svg?branch=master)](https://travis-ci.org/Soneritics/Realworks.svg?branch=master)
[![Coverage Status](https://coveralls.io/repos/github/Soneritics/Realworks/badge.svg?branch=master)](https://coveralls.io/github/Soneritics/Realworks?branch=master)
![License](http://img.shields.io/badge/license-MIT-green.svg)

by
* [@Soneritics](https://github.com/Soneritics) - Jordi Jolink

## Introduction
This script connects to the Realworks Real Estate service.
It provides easy parsing methods for parsing the XML data into PHP objects, providing easy overrides using IOC (dependency injection).

## Conditions
The following conditions have been set by Realworks. As an ISP you will have to sign an agreement in which you agree to these. Just for the record, the list of the most important items is shown below as well.
 * The file may only be downloaded once per natural day (24 hours).
 * The new file should be downloaded after 8:30AM.
 * The file contains all data, changes and cancellations until the day before.
 * The objects may only be used on the broker's website.
 * Objects are in the XML until 7 days after cancellation.
 * Files and media may not be hot linked. Files should be downloaded to your own server.
 * Maximum size of the images is 1600x100 pixels.

## Minimum Requirements ##
- PHP 5.6+

## Examples
Minimal example, when you have downloaded and extracted the ZIP file yourself and only want the XML to be parsed:
```php
$type = new \Realworks\RealEstateType\Wonen;
$xmlFilename = __DIR__ . '/../test/Assets/wonen.xml';

// Parse the file
$xmlFile = new \Realworks\File\XMLFile($xmlFilename);
$parser = (new \Realworks\Parser\ParserFactory)->build($type);

$result = $parser->parse($xmlFile);
print_r($result);
```

This script can also guide you through the whole process, including:
 * Download the file
 * Validate the zipped content
 * Unpack the zipped content
 * Validate the XML file against the XSD
 * Process the XML file
The example for this is included as [FullExample.php](example/FullExample.php).
