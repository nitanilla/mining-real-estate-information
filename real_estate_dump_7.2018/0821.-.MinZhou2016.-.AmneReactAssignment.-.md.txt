# AmneReactAssignment
This is a React Assignment. Using to fetch all nearby real estate agencies of particular address in Austin.

* Author: Min Zhou
* **Github: "https://github.com/MinZhou2016/AmneReactAssignment"**

## Front-End Part
**URL: "http://awake-idea.surge.sh/"**

### Main Theory
The Main function is to let user input two address, and show the result to the map and list

* Based on two address user input, Do such things:
    * First: Use Google Map API to make sure the address can be found in Austin
    * Second: if true, get its correspoding geometry point.
    * Third: Based on the geometry point, use Google Places API, Get real estate within 10 miles of            either point
    * Fourth: Use Google Map distance library, get every estate's sum distance to two addresses
    * Last: Sort the distance, show it on web page

### Components
* Nav-Bar
    * Search form (redux-form)
* Google Map 
    * show all estates and input address using marker, Click the marker to get more info
* Real Estate List 
    * show all estates in ascending order of sum distance)



## Back-End Part
Main Function: Fetch real estates position data using Google Place service and offer it to front end.
