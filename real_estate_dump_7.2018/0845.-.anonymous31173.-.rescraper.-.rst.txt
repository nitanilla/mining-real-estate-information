rescraper.py
------------

Web scraper for realestate.co.nz_
`````````````````````````````````

*By Ian Witham*

Realestate.co.nz is the website run by the Real Estate Institute of New Zealand. It lists every property for sale or rent by every licensed real estate agent in New Zealand (which should be all of them).

It also lists the details of every real estate office and real estate agent in New Zealand.

This make it a valuable source of data and worth writing a web-scraping module for IMHO.

It is usable at the moment but please note that there are a few features left for me to add. As you may expect, any substantial changes to the structure of realestate.co.nz could break this module, but I'm hoping that comprehensive unit testing will mitigate that risk and make it easy (or easier) to adapt if necessary.

Dependencies
````````````

- Python 2.7.x

- Beautiful Soup 4 (pip install bs4)

.. _realestate.co.nz: http://realestate.co.nz
