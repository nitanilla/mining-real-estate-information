![N|Solid](https://terra-2017.herokuapp.com/favicon.ico)

# Terra
Terra is a React App with NodeJS/Express backend that finds the closest real estate agencies to any two places and lists them by proximity to the two addresses.
See it here: https://terra-2017.herokuapp.com/
# Internals:
### High Level Request Flow:
The front end uses Google Maps Javascript API for autocompletion of addresses. On entering the two addresses, a backend API call is sent to get the list of real estate agencies.

The backend API,
 - uses Google Places API to fetch nearby real estates within 10 miles radius of each address.
 - removes duplicates in the two lists
- fetches the distance to each of the address using Google Distance Matrix API (bulk API call).
- computes sum of distances to each place.
- sorts by smallest sum and returns a list of addresses back to the UI.

The front end then uses the Google Maps Javascript API to show the list of places in the Map.
The UI is built to be responsive.

### Tech

Terra is built on the following technologies:

* react.js - for front end
* node.js  and Expressjs - for server
* axios - for api calls
* config - for managing configuration
* heroku - for deployment
