## Real Estate Listings
https://real-estate-listings.herokuapp.com

API endpoint `/listings` returns a filtered set of real estate listings in the Phoenix, Arizona area. I built this API entirely with JavaScript. I used Express and PostgreSQL.

example: https://real-estate-listings.herokuapp.com/listings?min_price=100000&max_price=200000&min_bed=2&max_bed=2&min_bath=2&max_bath=2

#### query params:
* `min_price`: The minimum listing price in dollars.
* `max_price`: The maximum listing price in dollars.
* `min_bed`: The minimum number of bedrooms.
* `max_bed`: The maximum number of bedrooms.
* `min_bath`: The minimum number of bathrooms.
* `max_bath`: The maximum number of bathrooms.

The expected response is a GeoJSON FeatureCollection of listings:
```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {"type": "Point", "coordinates": [-112.1,33.4]},
      "properties": {
  "id": "123ABC",
  "price": 200000,
  "street": "123 Walnut St",
        "bedrooms": 3,
        "bathrooms": 2,
        "sq_ft": 1500
      }
    }
  ]
}
```
All query parameters are optional, all minimum and maximum fields should be inclusive (e.g. `min_bed=2&max_bed=4` should return listings with 2, 3, or 4 bedrooms).

* API endpoint URL is `/listings`; **GET** requests only
* API responds with valid [GeoJSON](http://geojson.io)
* API correctly filters any combination of API parameters
* Data is stored in a PostgreSQL database on Heroku


### Features I would like to add:
* Tests for code
* Pagination
* Nice looking landing page