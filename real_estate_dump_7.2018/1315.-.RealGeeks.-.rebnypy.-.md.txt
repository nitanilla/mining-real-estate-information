#rebnypy [![Build Status](https://travis-ci.org/RealGeeks/rebnypy.svg?branch=master)](https://travis-ci.org/RealGeeks/rebnypy)

This is a python client for the real estate board of new york.


## Installation

```bash
pip install rebnypy
```

## Get New Listings

Use the `get_new_listings` method with your username and password.  This returns an iterator, each item in the iterator is a python dictionary with the listing data in it.  All the lookup fields have already been looked up for you.

```python
import rebnypy

c = rebnypy.RebnyClient('http://idx-api.olr.com/api','MY_API_KEY')

for listing in c.get_new_listings(start_date = datetime.datetime.utcnow() - datetime.timedelta(days=1))
    print listing
```

## Get All Listings

Basically the same thing as get new listings, but returns all of them!

```python
import rebnypy

c = rebnypy.RebnyClient('http://idx-api.olr.com/api','MY_API_KEY')

for listing in c.get_all_listings()
    print listing
```

## Get a single property by mls_number

```python
import rebnypy

c = rebnypy.RebnyClient('http://idx-api.olr.com/api','MY_API_KEY')

c.get_listing_by_id(1234)
```

Returns a dictionary with the information from a single MLS number.  Looks up all the data for the lookup fields for you behind the scenes.


# Running tests
If you want to run the integration tests, you'll need a REBNY API key.  Set the following environment variable before running the tests:

 * REBNY_API_KEY

# Debugging
Configure the python logger to barf out DEBUG if you want the HTTP going over the wire, INFO if you just want more stuff about the queries being run

Just for kicks, here's how to turn on logging to the console for all loggers:

```python
console_log = logging.StreamHandler()
logging.getLogger().addHandler(console_log)
logging.getLogger().setLevel(logging.INFO)
```

# Changelog
* 1.0.1: Fix bug with single listing
* 1.0.0: Remove `hours_previous`, pass a `start_date` instead.
* 0.1.2: Fix lookup for Status
* 0.1.1: Expand sub-dictionaries for lookups
* 0.1.0: Strip all values that are just None
* 0.0.3: Fix bug bug with new listings datetime
* 0.0.2: Actually expose RebnyClient in the module
* 0.0.1: initial release

# License

The MIT License (MIT)

Copyright (c) 2015 Kevin McCarthy

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
