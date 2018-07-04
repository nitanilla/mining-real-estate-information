TogetherMap
===========

## A web and mobile app for collaborative mapping

TogetherMap is intended to be the Google Docs-style app for editing and sharing shapefiles.

An instance of TogetherMap is hosted on [togethermap.com](http://togethermap.com), and you can load collections with up to 5000 shapes there, but if you want to use it to host data for your own organization (which is very much allowed), you can use the install instructions below to install an instance you control on your own servers.

**TogetherMap utilizes Meteor/Mongo on the backend and the Meteor/Mapbox stack on the font - think web maps backed by a trivial-to-install database and you have the right idea.  If you're looking for all the bells and whistles for managing spatial data in Meteor/Mongo, TM has a good start on many of them.**

Main implemented features include:
* GUI import and export for small collections
* Command line import and export for large collections, easy scripting access using PyMongo
* Incredibly fast export from Mongo to Pandas DataFrames using Monary
* Easy deploy of TM and MongoDB using Meteor deployment tools
* Digest emails for updates by collection using MailGun
* Synchronized mapping comes built-in for Meteor apps
* Synchronized commenting on places
* Read, Comment, Place addition, and Owner per-collection permissions using Google-docs style email links
* Theming functions in Javascript, multiple themes per collection
* Meteor templates to configure how to display place data in HTML
* Meteor autoform to use HTML forms to receive data edits from users
* Server- and client- side filters to load only the data you need
* Mapbox Vector Tile server built-in with server-side caching (MapBoxGL.js ready)
* Full site tested and configured for mobile, deployable to app stores using Meteor tools

It is a work in progress.  It is a side project, and is only tangentially related to my job, so please keep that in mind when making requests.  That said, don't hestiate to ask as I do enjoy the work.

## Documentation

Documentation is available [here](http://fscottfoti.github.io/togethermap_help/).  The most interesting part of that documentation to this audience is probably the discussion of how to [customize](http://fscottfoti.github.io/togethermap_help/customization/) rendering of places in TM, which is definitely a programming exercise - it uses Handlebars.js and Autoform extensively, as well as Javascript functions for theming and allows configuration of Meteor/Mongo filters via the interface.

## Installation

Installation is simple. 

* First [Install Meteor](https://www.meteor.com/install)
* Second clone this repo
* Third run `meteor` in the cloned repo
* Fourth open up `http://localhost:3000/` in a web browser

## Deployment

Deployment is a bit beyond the context of this document.  Meteor has standard tools for this though, so if you're a savvy programmer feel free to give it a shot and ask questions as I've encountered and solved quite a few deployment issues.  **If you're not a programmer, I'm happy to help you set up and deploy TM for a reasonable consulting fee.**

## Loading Sample Data

Docs on how to import and export geojson and shapefile data using Python are in this section.

### Import into TM

First this assumes you are in the `scripts` directory so feel free to `cd scripts`

To import json data in the form of one geojson feature per line (which keeps you from having to hold all features in memory at the same time or to wait until the entire geojson file is loaded), just run:

`python tmimport.py sample_data/us_states.json`

To load the same data as a standard geojson file run:

`python tmimport.py sample_data/us_states.geojson`

Note that the [tmimport.py](https://github.com/fscottfoti/togethermap/blob/master/scripts/tmimport.py) utility assumes the data is in one format or the other based on the filename ending.  It doesn't auto-detect the format or anything.

To load from shapefile, just run (this uses the Fiona library so make sure the library and its dependencies are installed):

`python tmimport.py sample_data/ZillowNeighborhoods-HI.shp`

Note that the [tmimport.py](https://github.com/fscottfoti/togethermap/blob/master/scripts/tmimport.py) script creates a new collection every time it loads one of these files and uses the new collection to hold the places from the file.  

You might need to edit the code in order to use the non-default port and database for the TM app and for the MongoDB.  These will be configuration options at some point in the future.  It's a pretty simple script at this point, so open it up and knock yourself out.

An especially fun import script is the [example](https://github.com/fscottfoti/togethermap/blob/master/scripts/web_parsing_example.py) which parses data directly from [the best restauruants in Portland by Eater](http://pdx.eater.com/maps/best-portland-restaurants-38) using the Python library Beautiful Soup. 

A very common [use case](https://togethermap.com/collection/ecGPcWi4XRDvMHLSp) for TM is to load place lists into TM using images and links - this [example](https://github.com/fscottfoti/togethermap/blob/master/scripts/load_custom_json_example.py) uses Curbed data on new development projects which is in a custom json [format](https://github.com/fscottfoti/togethermap/blob/master/scripts/curbed-sf.json).

### Export out of TM

Export in TM is just as simple.  Just run [tmexport.py](https://github.com/fscottfoti/togethermap/blob/master/scripts/tmexport.py) with the collectionId and file format as the two arguments.  The collectionId is a hash which is unique to each collection.  For instance, the collectionId for this [collection](https://togethermap.com/collection/ecGPcWi4XRDvMHLSp) is `ecGPcWi4XRDvMHLSp` (just get it from the URL).  The format can be one of `json`, `geojson`, or `shp` in order to create the three file types.  Remember from above that json creates one geojson feature per line while geojson is proper geojson.

Another awesome export script is this [example](https://github.com/fscottfoti/togethermap/blob/master/scripts/export_to_pandas.py) which uses the Monary library to export from MongoDB to Pandas DataFrame in the most efficient way possible.  This can create a DataFrame for millions of documents/rows in 20-30 seconds depending on how many features are specified to be exported.

## A Note on Meteor

Meteor is a JavaScript framework (created by a friend of mine from high school, and now with 10s of millions in funding) which allows real time transfer of data from a MongoDB to web and mobile clients.  In my opinion, it's real strength is to put client and server in the same language, side by side, and to allow data access in both client and server using the same abstractions (which are both based on Mongo).

Perhaps even more importantly, the ease of installation, of managing Javascript packages, and of deployment has really been a timesaver for me.  That said, the frontend framework for Meteor, called Blaze, is very clean but perhaps not as powerful or familiar as frameworks like React and Angular.  As Meteor now seems set for a move to React, I think TM might be headed in that direction, but for now everything is in the vanilla Meteor stack.

## Why not Postgres?

Let's get this one out of the way: why not back with a Postgres/Postgis db?  Honestly, for two reasons.  1) Postgres is a bear to install and 2) maintaining schemas across application contexts is an enormous pain.  In my opinion, it's about time for geo to move to the web paradigm = json documents and filters on collections rather than relationships, and do geo analysis in Python.  The day might not be today, but it's coming.  Of course, many important projects are built on Postgis today, so including Postgis connectivity as an option makes a ton of sense (it doesn't yet exist).

## Parts of TM that require other services

It should also be noted that almost all tools used in TM are open source and therefore free - this includes everything in Meteor, Mapbox, and TM itself.  The only exceptions are:

* A Mapbox key can be provided in order to access Mapbox basemaps, markers, and a few other items, although it's not required.
* If you want to do more than run locally, deployment must be paid for.  If you have an Amazon EC2 instance you can run on any Ubuntu machine.  I also use a Digital Ocean instance for $5/month and a MongoDB instance at compose.io for about $18/month, so deployment cost is modest.  Really anything that supports deployment of Meteor apps should work.  Or you can just load and customize collections on togethermap.com.
* Filepicker.io is used to manage images in TM, and is a wonderful tool to allow connectivity to lots of cloud based storage providers.  They keep raising their prices and it's now up to $99/month for any substantive use, so it's almost certainly on its way out of TM.

## Meteor/Mongo Data Schema

There are currently four Meteor/Mongo collections.

Let's get one terminology issue out of the way up front.  Collections in TogetherMap are a set of places that embody a common theme, similar to a layer in GIS (e.g. States in the United States).  Collections in MongoDB are sets of JSON documents.  All places in every TogetherMap collection are stored in a single MongoDB collection called Places.  There is also a MongoDB collection called Collections which describes settings for each TogetherMap collection.  This is subject to change in the future, but I just like the term "collection" more than "layer" inside of TogetherMap.  In almost every place in this documentation I think the intended use of the word collection is fairly obvious, but this section is undoubtably confusing and lame.  Bear with me.

* Collections - The Collections collection stores a single document per TM collection which configures that collection, and includes information like name, description, the user who created the collection, number of places in the collection, and information on how to theme the collection.
* Places - places are geojson objects which store your spatial data.  That's right, all shapes are in the same collection.  Many millions of them if you want.  Filter on the collectionId attribute (which relates to the _id attribute in the Collections collection) to access all the places for a TM collection.
* Followed - a set of documents which keeps track of which collections a user is following.  This could probably by user data (i.e. in the Meteor Users collection), but it's not right now.
* Comments - a set of documents which keep track of the comments on a given place using the placeId attribute (which relates to the _id attribute in the Places collection).

## Vision for Future Work

* Mobile app - although you can go to a TM website and use it perfectly well on any mobile device, releasing a mobile app in the app stores has not been done yet.  Meteor is designed to deploy to Android and IOS and I have successfully prototyped this, but a small amount of cleanup is still required for an initial release.
* Mapbox.js - TM now supports being able to serve Mapbox Vector Tiles in compressed format and with caching on the server.  Initial prototypes show that Mapbox GL (a WebGL library) can take these tiles from TM and render 10s of thousands of shapes with no lag.  This is clearly the future of TM (and web mapping in general) and I look forward to integrating more tightly with TM collection configuration options.
* I work closely with city and regional land use and transportation planners (I'm current employed by MTC in the Bay Area).  As such my primary use case is to visualize parcels shapes and attach zoning attributes to those shapes.  The main functionality here is just being able to join a second csv file to a collection of shapes, and this is a common operation in GIS too.  This isn't supported yet in TM but should be soon.
* Along those lines, I use TM to do a ton of visualizations for analyses on where future real estate developments are likely to be located (based on current markets and some addtional forecasting).  I will continue to improve the workflow to get TM data into Python for analysis and then into TM for visualization and feedback.  In the future I can imagine adding interactive charting of collection attirbutes similar to the [UrbanLayers](http://io.morphocode.com/urban-layers/) demo.

## Note on Testing

Yup, there's no tests.  I'm not, like, against tests or anything, I just don't require a 24/7 always-on app for my work.  I'd love to have the justification to start writing tests, but need to find out if anyone will use the app first before spending my nights and weekends building a bulletproof app that no one uses.  If you want tests, don't get uptight or mean, just open an issue and/or do the usual "+1" voting.  Or better yet, pitch in.
