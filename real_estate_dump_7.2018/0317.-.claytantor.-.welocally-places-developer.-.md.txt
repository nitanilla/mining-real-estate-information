README v 1.1.8
=================

Basic documentation include in examples/demo.html

What is a Welocally Place?
============

Welocally Places For Developers is a set of jQuery based javascript widgets that make it 
easy to create highly styled customized maps using Google Maps API v3. Its perfect for 
creating business directory websites, travel sites, real estate guides or any website 
where you want to go beyond the look and feel of Google Maps and showcase real world places.

It is founded around the data of places. Simply put, a place is all the relevant facts 
about a real world location, like its name, location, phone number, and website. This 
data is then used to set the map location and create place cards or marker maps.

```javascript
//places are an array of JSON objects
var places = [
  {				                       
      "properties": {
          "phone": "+1 510 595 8000",
          "classifiers": [
              {
                  "category": "Restaurant",
                  "subcategory": "",
                  "type": "Food & Drink"
              }
          ],
          "titlelink": "http://oaklandly.com/sicily-pizza",
          "website": "http://www.sicilypizzapasta.com",
          "address": "138 14th St",
          "name": "Gourmet Sicily Pizza",
          "province": "CA",
          "owner": "welocally",
          "postcode": "94612",
          "country": "US",
          "city": "Oakland"
      },
      "geometry": {
          "type": "Point",
          "coordinates": [
              -122.2636,
              37.801379
          ]
      }
  }
];
```

Our primary goal is to combine a number of aspects of the Google Maps API into a single easy to 
use set of components, helping developers build beautiful and unique hyper-local websites 
with ease.

Place Widget
============

The place widget creates a pin card for a specific place. It perfect for showcasing a specific 
location. Of course all of the Google Maps Capabilities work also, so users can use street 
view to get curb appeal quickly.

```javascript
//config for the widget
var cfg = { imagePath: 'images/marker_all_base.png'};

//instantiate it
var placeWidget = 
  new WELOCALLY_PlaceWidget(cfg)
    .init();

//load loacally with local place
placeWidget.load(places[0]);
```

Multi Places Widget
=====================

The multi places widget will automatically scale to the correct view bounds to include all 
the place markers. When a user selects a specific place marker details like website or phone 
number and driving directions become visible and the map will center. This map is great for 
creating a set of places with a specific category, such as "Shopping" or a travel map.

```javascript
//used for the place display when selected (observed)
var placeSelected = new WELOCALLY_PlaceWidget({}).init();

//config the widget, use the places array
var cfg = { 
 id:'multi_map_1',
 imagePath: 'images/marker_all_base.png',
 observers:[placeSelected],
 places: places
};

//it both objects 
placeSelected.initCfg(cfg);
var placesMulti = 
	  new WELOCALLY_PlacesMultiWidget(cfg)
  		.init(); 

//setup the selected area, display selected
placesMulti.getSelectedArea().append(
  placeSelected.makeWrapper());
```

