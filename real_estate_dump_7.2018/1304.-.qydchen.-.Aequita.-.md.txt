# Aequita

Aequita is a data-visualization infographic that plots recent home sales price data by neighborhood. This infographic aims to show a concept that can be expanded as a tool for various professionals working in real estate and finance, as well for home-seekers who are looking for comparable home pricing.

## Implementation

### Gathering data

The recent home sales price data in NYC is obtained from http://www1.nyc.gov/site/finance/taxes/property-rolling-sales-data.page. The data is then manually filtered in Excel. The data will only include 1-3 family dwellings and date of sale will only be from Jan 2017 to May 2017. The real estate data will also exclude transfer of ownerships ($0 sale price) and oddly cheap sale prices ($10,000 for a 2-family home).

The excel database is cleaned and converted into a csv format in order to obtain latitude and longitude geolocations from the US Census api. Then the database is then converted into an array of objects from csv.

Below is a sample of the array:
```JavaScript
export const rollingSales = [
  {
    "ID": 2268,
    "ADDRESS": "1208 8TH AVENUE",
    "CITY": "Brooklyn",
    "STATE": "NY",
    "ZIP CODE": 11215,
    "LNG": -73.980804,
    "LAT": 40.663864,
    "NEIGHBORHOOD": "PARK SLOPE",
    "BUILDING CLASS CATEGORY": "03 THREE FAMILY DWELLINGS",
    "LAND SQUARE FEET": "1,284",
    "GROSS SQUARE FEET": "2,080",
    "YEAR BUILT": 1899,
    "SALE PRICE": "1,670,000",
    "SALE DATE": "4/20/17"
  },
  {
    "ID": 2269,
    "ADDRESS": "1372 EAST 24",
    "CITY": "Brooklyn",
    "STATE": "NY",
    "ZIP CODE": 11210,
    "LNG": -73.95091,
    "LAT": 40.617313,
    "NEIGHBORHOOD": "MIDWOOD",
    "BUILDING CLASS CATEGORY": "01 ONE FAMILY DWELLINGS",
    "LAND SQUARE FEET": "4,000",
    "GROSS SQUARE FEET": "2,730",
    "YEAR BUILT": 1915,
    "SALE PRICE": "1,675,000",
    "SALE DATE": "1/4/17"
  }
]
```

Along with a database of rolling home sales, a database of neighborhood geoJSON has to be loaded onto Google Maps api. The geoJSON data for the various Brooklyn neighborhoods are found here: http://catalog.opendata.city/dataset/brooklyn-neighborhoods-polygon/resource/7a0a136e-b7bb-44f5-8044-f21591ef49aa

Below is a sample of the geoJSON shape required to pass into Google maps:
```JavaScript
export const brooklyn = {
"type": "FeatureCollection",

"features": [
  { "type": "Feature",
    "properties": {
      "neighborhood": "Bath Beach",
      "boroughCode": "3",
      "borough": "Brooklyn",
      "@id": "http:\/\/nyc.pediacities.com\/Resource\/Neighborhood\/Bath_Beach" },
    "geometry": {
      "type": "Polygon",
      "coordinates":
      [ [ [ -73.99381, 40.601950000000194 ],
      [ -73.999619627195642, 40.5964689678977 ],
      [ -74.000471, 40.595939 ],
      [ -74.000167439243185, 40.595549476398048 ],
      [ -74.001844151354831, 40.593977667237887 ],
      [ -74.002003948093702, 40.59413237127562 ],
      [ -74.003634019473168, 40.596080599242953 ],
      [ -74.003974449525586, 40.596343011141563 ],
      [ -74.004178751373729, 40.596500492055917 ],
      [ -74.005526219861366, 40.597539154070802 ],
      [ -74.009217239049079, 40.59984404515253 ],
      [ -74.010901450535087, 40.60071555985418 ],
      [ -74.012369816027132, 40.601349257116311 ],
      [ -74.014783637167511, 40.60208210297089 ],
      [ -74.015625838923143, 40.602235351515411 ],
      [ -74.015626147147429, 40.602235407600325 ],
      [ -74.016182962982555, 40.602336726809881 ],
      [ -74.016526357899423, 40.602399211565917 ],
      [ -74.018323472168646, 40.602417651130637 ],
      [ -74.019135639028889, 40.602612754505159 ],
      [ -74.019434836341958, 40.602843501044902 ],
      [ -74.018641, 40.603655000000224 ],
      [ -74.019152335880349, 40.603819763783996 ],
      [ -74.018531, 40.604458000000228 ],
      [ -74.017467, 40.604965 ],
      [ -74.015499, 40.606842000000128 ],
      [ -74.01702, 40.60765500000025 ],
      [ -74.011726046282689, 40.612743758637301 ],
      [ -73.99381, 40.601950000000194 ]
    ]]}
  }]
}

```

### Creating borders

Loading geoJSON into Google Maps api is simple.

```JavaScript
  map.data.addGeoJson(geoString);
```

Further, we can give a listener to each area like so:

```JavaScript
  map.data.addListener('click', cb(event) {})
```

Within the callback, I created a Google Maps api Polygon class that will be the same as the neighborhood. That polygon will then be used as a filter to fetch homes in that area.

```JavaScript
  let neighborhoodGeo = event.feature.getGeometry();
  let neighborhoodPoly = new google.maps.Polygon({
    paths: neighborhoodGeo.getAt(0).getArray(),
    map: map,
    clickable: false,
    visible: false,
  });

  initMapMarkers(map, neighborhoodPoly);
```

### Making markers
Upon clicking on a neighborhood polygon, the callback will run a function named `initMapMarkers`:

```JavaScript
export function initMapMarkers(map, neighborhoodPoly){
  clearMarkers();
  totalSalePrice = 0;
  totalSqFt = 0;
  rollingSales.forEach(home => {
    createHomeSaleMarker(home, map, neighborhoodPoly);
  })
};
```

If there are any markers already on the map, clear the markers and then fetch new markers associated to the new selected neighborhood.

`totalSalePrice` and `totalSqFt` are variables used to store the sum for aggregate data for the neighborhood polygon.

`rollingSales` is the JS array of objects that contains recent home sales.

### Creating an individual marker

When creating a marker, we have to pass in a `{lat, lng}` in order to tell Google Maps api where to plot the marker.

```JavaScript
function createHomeSaleMarker(home, map, neighborhoodPoly) {
  const image = "https://s3.amazonaws.com/safehavns-dev/smart-home.png";
  const lat = parseFloat(home["LAT"]);
  const lng = parseFloat(home["LNG"]);
  const latLng = new google.maps.LatLng(lat, lng);
  if (google.maps.geometry.poly.containsLocation(latLng, neighborhoodPoly)) {
    var marker = new google.maps.Marker({
      position: {lat, lng},
      icon: image,
      map: map,
      id: parseInt(home["ID"])
    });
    bindInfoWindow(marker, map,
      "<div class='infowindow'>"
      + "Address: " + home["ADDRESS"] +
      "</div>" +
      "<div class='infowindow'>"
      + "Sale Date: " + home["SALE DATE"] +
      "</div>" +
      "<div class='infowindow'>"
      + "Sale Price: " + home["SALE PRICE"] +
      "</div>" +
      "<div class='infowindow'>"
      + "Building Class Category: " + home["BUILDING CLASS CATEGORY"] +
      "</div>"
    );
    totalSqFt += digitInputs(home["GROSS SQUARE FEET"]);
    totalSalePrice += digitInputs(home["SALE PRICE"]);
    homesMarkers.push(marker);
  };
};
```

Real estate professionals and analysts work with granular data. Likewise, a detailed `infowindow` will display more granular information for a specific home.

```JavaScript
  function bindInfoWindow(marker, map, html) {
    var infowindow =  new google.maps.InfoWindow({
      content: ''
    });
    google.maps.event.addListener(marker, 'mouseover', function() {
      infowindow.setContent(html);
      infowindow.open(map, marker);
    });
    google.maps.event.addListener(marker, 'mouseout', function() {
      infowindow.close();
    });
  };
```

Lastly, while iterating through and creating markers for a specific neighborhood, `totalSqFt` and `totalSalePrice` accumulates for aggregate calculations of that specific neighborhood. This will be used to populate the summary details on the top-left hand panel.

```JavaScript
export function appendStats() {
  let stats = {};
  stats.totalHomes = homesMarkers.length;
  stats.asp =
    Math.round(totalSalePrice/stats.totalHomes) ?
    numberWithCommas(Math.round((totalSalePrice/1000)/stats.totalHomes)) :
    null;

  stats.avgsqft =
    Math.round(totalSqFt/stats.totalHomes) ?
    numberWithCommas(Math.round((totalSqFt/10)/stats.totalHomes) * 10) :
    null;

  stats.pricePerFt = Math.round(totalSalePrice/totalSqFt) ?
    numberWithCommas(Math.round((totalSalePrice/totalSqFt))) :
    null;

  let aspTxt = stats.asp ? "Avg. Selling Price (000's): $" + stats.asp : "N/A";
  let avgsqftTxt = stats.avgsqft ? "Avg. Sq. Feet: " + stats.avgsqft + " sq. ft" : "N/A";
  let pricePerFtTxt = stats.pricePerFt ? "Avg. Price/Avg. Sq. Feet" + stats.pricePerFt : "N/A";

  document.getElementById('total-homes').textContent = "Total Homes Sold: " + stats.totalHomes;
  document.getElementById('asp').textContent = aspTxt;
  document.getElementById('avgsqft').textContent = avgsqftTxt;
  document.getElementById('priceperft').textContent = pricePerFtTxt;
};

```

## Methods of Optimization

### Bounding Boxes
Upon selecting a neighborhood, the code snippets written above currently iterates through the entire rollingSales data and compares each `lat` and `lng` to each polygon coordinate. For these polygons, I created 'bounding' boxes for each in order to reduce the number of iterations on each selection.

```JavaScript
  export function getBoundBoxFromPoly(neighborhoodPoly) {
    let polyArrays = neighborhoodPoly.latLngs.b[0].b
    let minLat = null;
    let maxLat = null;
    let minLng = null;
    let maxLng = null;
    polyArrays.forEach(_f => {
      let lat = _f.lat();
      let lng = _f.lng();

      if (lat > maxLat || !maxLat) {
        maxLat = lat;
      } else if (lat < minLat || !minLat) {
        minLat = lat;
      }

      if (lng > maxLng || !maxLng) {
        maxLng = lng;
      } else if (lng < minLng || !minLng) {
        minLng = lng;
      }
    })
    return {minLat, minLng, maxLat, maxLng};
  }
```

With this way, the program iterates through the array and only have to compare against 4 corner coordinates of a rectangle instead of multiple points on an irregularly shaped polygon.

### Memoization

Memoization is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again. In this context, bounding boxes are associated to a `neighborhood`, and each bounding box has several hundred markers to iterate through. Using memoization, an empty object is created, and at each fetch into the database, the result is stored in the object for faster fetching.

```JavaScript
  let filteredSales = {};

  export function initMapMarkers(map, neighborhoodPoly, neighborhood){
    clearMarkers();
    totalSalePrice = 0;
    totalSqFt = 0;

    let boundBox = getBoundBoxFromPoly(neighborhoodPoly);
    if (!filteredSales[neighborhood]) {
      filteredSales[neighborhood] = rollingSales.filter(function(home){
        const lat = parseFloat(home["LAT"]);
        const lng = parseFloat(home["LNG"]);
        return (lat > boundBox.minLat
          && lng > boundBox.minLng
          && lat < boundBox.maxLat
          && lng < boundBox.maxLng
        )
      })
    }

    filteredSales[neighborhood].forEach(home => {
      createHomeSaleMarker(home, map, neighborhoodPoly);
    })
  };
```

## Questions?

I hope this project and instruction will pave the way for another up-and-coming developer to explore the power of Google Maps api. This project has many commercial use cases ranging from data analytics to home buying. Feel free to reach out if there are any questions/concerns.
