# AMNE_RE_Finder

To run this app locally:

1. Clone repo and run npm install
2. Get a gMaps api key at https://developers.google.com/maps/documentation/javascript/get-api-key
3. Enable the following 3 API's for your key:
    - Google Maps Geocoding API
    - Google Places API Web Service
    - Google Maps Distance Matrix
4. Create a .env file using .env.example as guideline and paste your google API key under "GMAPS_API_KEY"
5. Open 2 terminal instances from the root of this project: 
    - in one run the command "npm start"
    - in the other run "node ./nodeServer/server.js"
6. You can now access the project at http://localhost:8080


General flow:

 - accept input addresses
 - send addresses to Google Maps Geocoding API 
    + receive the latitude/longitude coordinates for each address
 - send coordinates along with other necessary parameters to Google Places API
    + receive all real estate agencies within a 10 mile radius of coordinates
 - take real estate agency addresses and original input addresses, and send them to Google Maps Distance Matrix API
    + receive the distances from each real estate agency to each input address
 - sum the distances of each realestate agency to each original address
 - sort real estate agencies by summed distance
 - render real estate agencies in ascending order of distance