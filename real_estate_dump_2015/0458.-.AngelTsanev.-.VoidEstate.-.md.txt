VoidEstate
==========

Android application for real estate sales...



VoidEstate is a mobile application for Android for real estate sales.
It connects to SQL database server through php myAdmin. The main screen shows
map of Bulgaria (using google maps) and markers are placed for every estate
in the database. The map can be zoomed in and out. Each marker can be clicked
and shows short information about the estate it represents. The info window
can then be clicked to send the user to new screen which shows detailed information
about the estate. The user can then call the agent, email the agent or see the
estate on the map. On the first screen (the map) there is a search button.
When clicked it opens a new screen which contains criterias for searching like
price range, city, distance to city (radius), number of bedrooms and size. When 
the search criteria is set the user can click on the search button. Then VoidEstate
connects to the database server and executes the search query. At that point a new
screen opens where he can see all estates meeting his criteria. They are shown as a
simple list with short information such as ID, price and description. The user can
then click on every entry of the list he likes and the application opens the screen
with detailed information for that estate.
