## Recovery: US Housing Trends ##

#### Authors: Renzo Lucioni and Kathy Lin ####

[Screencast](https://www.youtube.com/watch?v=vbEo6OinpqE)

### Overview ###

This repository contains the code and data used to create a clean, useful, and insightful interactive visualization which can be used as a tool for exploring recent trends in the US housing market.

### Run ###

To run our visualization, run the following *while at the top level of the directory*:

```bash
$ python -m SimpleHTTPServer
```

Then, in your browser, visit `http://localhost:8000/code/recovery.html`.

### Directory Structure ###

As you might expect, the `code` directory contains our project code. Within `code`, the `coffee` directory contains our [CoffeeScript](http://coffeescript.org/) code, the `js` directory contains compiled, human-readable JavaScript, and the `css` directory contains our custom styling. All required libraries are linked in `recovery.html`. The Python script `augment-topojson.py` is used to meld US housing market data with a TopoJSON file; `process-nationwide-data.py` is used to pull national data from Zillow's metro-level datasets.

The top level of the `data` directory contains several JSON files, a collection of CSV files, and a TSV file. Within `data`, the `zillow` directory contains a collection of CSV files downloaded from [Zillow Real Estate Research](http://www.zillow.com/research/data/). To indicate its granularity, the data itself is located within either the `county` or `metro` directories nested within `zillow`. Three of the TopoJSON files contained in `data`, `us-states-and-counties.json`, `augmented-us-states-and-counties.json`, and `compressed-augmented-us-states-and-counties.json`, define the paths of US states and counties; `augmented-us-states-and-counties.json` and `compressed-augmented-us-states-and-counties.json` include additional information extracted from the county-level Zillow CSVs and associated appropriately with each county. The JSON files named `nationwide-data.json` and `compressed-nationwide-data.json` contain information on national trends extracted from the metro-level Zillow CSVs. As you might expect, both `compressed-augmented-us-states-and-counties.json` and `compressed-nationwide-data.json` are significantly smaller than their uncompressed counterparts; this is a result of being structured differently. Finally, the sole TSV file, `us-county-names.tsv`, maps US counties to their [FIPS](http://en.wikipedia.org/wiki/FIPS_county_code) codes.
