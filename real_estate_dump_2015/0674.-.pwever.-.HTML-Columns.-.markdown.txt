

# HTML Columns

## Description

I was looking for a way to gracefully handle different browser text and window sizes. This test _columnizes_ given content elements in order to take advantage of the available screen real estate. It works for both text-only, text with inline images, and image grids.

## Supported browser

* Safari 5+
* Chrome 5+
* Firefox 3.5+

## Gracefully fails in

* Internet Explorer
* Opera

## Dependencies

* JQuery

## Known problems

* Inline images will can be split in two (or more columns).
* Since we are actually duplicating content for each additional column, copy/paste activities will most likely include duplicates.

## Todos

* Test and support more browsers.
* Compare and contrast with browser specific colum options (-moz-column-count etc.)
