LocalVector Maps
=================
LocalVector Maps is an interactive real estate data visualization tool that uses colorful choropleth maps and graphs as an intuitive approach to help residential real estate buyers quickly absorb a large amount of data in order to compare trends, identify specific high growth areas, visualize market recovery since the most recent meltdown, and explore homes currently for sale within five Bay Area counties. My goal was to build a unique real estate research tool that was intuitive and easy to gain a high level, comparative overview of the landscape but also offer enough granularity to be able to drill in and identify specific opportunities.

The application uses over 200,000 rows of licensed Multiple Listing Services real estate data as well as geospatial data from the US Census Bureau. This project will be incorporated as a new feature in the website of LocalVector, a Bay Area real estate search engine.

I built this application because I noticed a lack exploratory tools for non-professional investors like the mom-and-pops, particularly tools that presented data with maps focused on change over time in addition to price level snapshots. While line graphs are popularly used and also certainly show growth, they are limiting in granularity and the number of regions that can be compared in a single visualization.

Developed in 3.5 weeks at Hackbright Academy's Software Engineering Fellowship in the Spring 2014 cohort. 

#####Note on cloning this repository:
Note that this application uses licensed Multiple Listing Services (MLS) data, it is not possible to run this repository locally on your machine. The link will be posted once the app is successfully integrated into Local Vector. 

#####Technology used:
This application is built using the Flask framework and is written in Python in the back-end, Javascript in the front-end, and uses a PostgreSQL database.

1. Front-end: Javascript, jQuery, AJAX, HTML, CSS, Bootstrap, D3
2. Back-end: Python, Flask, SQLAlchemy, PostgreSQL, numpy module
3. GIS-related: Leaflet API, Mapbox, QuantumGIS, GeoJSON, Python shapefile library, markercluster library

Summary of Features
-------------------

![Main page](/screenshots/2salespricepage.JPG)
![yoy page](/screenshots/1YoYpricechange.JPG)

#####1. Choropleth Map 
The map offers visualization of 3 different metrics split out by zipcode. A button in the control panel on the left toggles off the choropleth layer if users need a clearer view of the map. For a more intuitive experience, the controls showing the metric options disappear when the user toggles off the choropleth. The three metric options displayed on the map are:  
  *	Median sales price of homes by zipcode
  *	Median sales price per square foot by zipcode
  *	Percent change in median sales price between any two years of the user's choice 
      *	This uses a diverging color scheme instead of a sequential one as in the metrics above. 
      *	The Python script ensures a minimum number of houses in each region for a more accurate representation of the data.

#####2. Range slider for year on year comparison
  * When a user selects the third metric (price change comparison) to view, a range slider appears that allows a selection of any base year and comparison year to view the % change in median price between the two years across all regions. 

#####3.	Information boxes on mouseover
  * When the mouse hovers over any region, the region is highlighted and an information box on the upper right corner appears to drill down into additional details about the region such as median price and number of homes sold, and exact % change where appropriate.
  * The Price Comparison option view shows in the mouseover information box a time series graph displaying the median price/sqft each year for the respective region.
  * Clicking on any particular region automatically zooms in to pull the region into the full viewport.

#####4.	Legend 
  *	The legend updates dynamically with the dataset with a clear label that updates based on the metric and years selected giving the user a clear understanding of what is displayed.
  *	The code allows the legend to automatically scale with the range of any particular dataset that the user chooses to view.

#####5.	Toggle to view homes currently for sale
  *	In the control panel on the left, a button allows the user to toggle on markers for active listings. When the users click on the markers, a pop-up displays showing detailed listing information including list price, address, # of beds/bath, a description of the property, and the MLS listing number. Users can click on the address and be taken to a separate detailed listings page  
  *	The display uses a markercluster library to avoid overwhelming the user with too many markers and improve performance. When the user mouses over a particular cluster, a polygon appears on the map indicating what area of the map the cluster covers. Clicking on the cluster automatically zooms into the map and splits clusters out into smaller clusters or map pins. Double clicking zooms back out to the original view.   
![Other page](/screenshots/1-activelistings.JPG)
![Local page](/screenshots/11-activelistings2.JPG)

Project Walk Through
--------------------
###Planning
######Leafletjs, Mapbox tile server, OpenStreetMap

With no prior experience in GIS or cartography, this project proved to be a test of resourcefulness in finding, understanding, and selecting the right GIS tools within the time constraints. Another big task was determining what geo and real estate data to use and how to display it on the map. 

With only 3.5 weeks to build the project, I had to be selective on what I wanted to focus on. Because of the nature of this application, I chose to focus on optimizing for speed. Users aren't likely to wait for more than 2-3 seconds for the map visualization to update. 

The application uses the Leaflet Javascript library for mapping applications, the Mapbox API for basemap tileserving, and OpenStreetMaps for the base mapping data. I built some preliminary applications using the Google Maps API and explored Mapbox and CartoDB's libraries, but Leaflet had more features and 3rd party libraries I could use for customizing a map, had excellent documentation, and because it's open source, I didn't need to worry about Terms of Service. 

Choropleth maps are thematic maps in which areas are shaded or patterned in proportion to the measurement of statistical variable. They're similar to heatmaps, though I chose not to use heatmaps because they reflect the density of data points in a region in addition to values, which would not have been an accurate representation of the data for the purposes of this project. This is how all the heatmaps libraries for cartography behaved.

In terms of granularity of detail, I felt that either the zipcode or neighborhood level would be granular enough without being overwhelming and ultimately settled on zipcodes as neighborhood boundaries were less clear cut. I chose  3 metrics: 1) sales price for those with a specific budget in mind, 2) sales price per square foot to normalize for an apples-to-apples comparison, and 3) price % change between any two years of the user's choosing between 2006-2013 to visualize trends over time. 

###Acquiring and Parsing Real Estate and Geo Data
######QuantumGIS, Shapefile library, Mapquest Bulk Geocoder, PostgreSQL, SQLAlchemy
A bulk of the work involved finding and preparing the geodata and real estate data to be used for the web application as well as figuring out how to structure my data model to most efficiently store and query the data.

I found that the US Census Bureau has large shapefiles gigabytes in size containing geospatial data including the latitude and longitudinal pairs of the polygon vertices to draw each region (zipcodes, block groups, etc) onto a map throughout the US. Many of the regions consist of hundreds of vertices and multiple separate polygons. 

I learned how to use an open source geographic information system called QuantumGIS to quickly visualize the shapefiles and convert them to a GeoJSON format for displaying as a layer on the map. I also used the Python shapefile library to extract data from the shapefile and seed into my database where I then trimmed the unnecessary regions. I wrote another Python script to modify the GeoJSON to extract a subset of the data once I determined those regions from the previous step in the process. 

A major task was designing the structure of the database to store all the latlong data so it could be easily and efficiently accessed, particularly to be able to run a Ray Casting algorithm that determines the membership of each home in the appropriate region, be it block group, census tract or subcounty.  

As for the real estate data, I used the Python csv module to seed the MLS data of over 200,000 homes into my database, while validating, cleaning and normalizing the data. I then used a Mapquest tool to bulk geocode all the addresses to latlong tuples for placement on the map.

###Displaying Data with Performance in Mind
######AJAX, JQuery, GeoJSON, numpy

I had originally used a Leaflet feature that drew each region's polygon by feeding my latlong data from the database to the client, but identified this as a major performance bottleneck. I researched and found another method that used GeoJSON files so that the frontend could handle all drawing of each polygon and avoided making extra server calls. While this increased the speed, it was still slower than I would have liked. I then switched to using a simplied version of the shapefiles with reduced accuracy by reducing the number of vertices while still retaining the shape integrity of each region. As a next step for the future, I'd want to adopt PostGIS for faster rendering and to further improve performance by avoiding drawing hundreds of polygons altogether, I would use a tool called Tilemill to style the tiles ahead of time. 

Next, I wrote a number of scripts to pre-calculate the various metrics I planned to display on the map using the Python numpy module. I had originally coded the server side to calculate these metrics dynamically with each client request, but found this affected performance negatively. I updated my database model and wrote the scripts to pre-process and store as much of the metric calculations in the database ahead of time as possible, including the medians of the total price, price per square foot, and number of homes sold broken out by region and time period. As I plan to build out more features and filters in the future that allow many combinations of options for the users, it would not be as efficient to pre-compute everything. I would likely need to consider optimizing the balance between pre-calculations, server-side, and client-side computations.

Another complication was how to pass the relative values to render the appropriate color in each region. Normally, the API assumes the values are embedded in the GeoJSON. However, in my case, the map can display various subsets of data and rendering a different GeoJSON for each dataset would have been time-consuming and inefficient. I used an AJAX call to a handler that created a separate JSON with just the relative values to then link together with the GeoJSON data on the client side. 

######Markercluster library

Initially, I tried rendering the active listings as individual markers but having the Leaflet API draw each marker individually was another performance bottleneck. I investigated other rendering techniques such as UTFGrids and markerclustering, ultimately deciding on the latter. This not only improved the speed but also the user experience and navigation. While the markerclustering library is handling the rendering and animation, I needed to prepare the data to be rendered and figure out how to pass it correctly and quickly to achieve this result. I initially used Jinja, the method taught in Hackbright's curriculum to pass data from the back-end to the front-end but switched over to JSON and AJAX techniques to improve efficiency. 

######Jquery UI, Bootstrap, D3

On the front-end I used the Jquery UI library for the range slider, bootstrap to style the buttons, Mapbrewer to select the colorscheme, and D3 for the time series graphs.

Sample Data Insights
--------------------
Here is a sample scenario of how a user might find insight from this tool and use it to then research possible homes to purchase.

By 2009-2010, real estate home values had reached bottom and the peak in home values was in 2006. This is clear from the warm colors covering the map, indicating widespread home value loss when you select 2006 as the base year and 2009 as the comparison year. 
![Loss] (/screenshots/3-2006-2009.JPG)

In recent years, real estate values have been recovering, apparent from the overwhelming green when 2011-2013 is selected on the range slider. When you hover over the regions for drill-down, you can see growth is especially strong near San Francisco, around Palo Alto, and Monterrey. 
![Growth] (/screenshots/4-2011-2013.JPG)

By comparing each of the years of 2010-2013 to the baseline of the 2006 peak in home values to gauge whether prices have returned to previous highs, you'll notice a single, rapidly growing green hot spot over time centered around Mountain View and Palo Alto. This indicates those regions have median home values that are now exceeding 2006 highs and are growing at a faster pace than the areas around San Francisco and Monterrey, which have not yet returned to previous highs. This likely is an effect of the strength of the tech industry in recent years. 
![Improving] (/screenshots/6-2006-2011.JPG)
![Improving More] (/screenshots/8-2006-2013.JPG)

You might then speculate the homes currently for sale around the fringes of the growing green hotspot have the most potential for growth (as well as near San Francisco and Monterrey) and investigate homes currently for sale by toggling on the active listings. 
![Searching] (/screenshots/9-2006-2013 with clusters.JPG)

Possible Expansions
-----------------
#####Predictive Analytics

The next step would be to build in predictive analytics that estimate growth potential based on leading indicators and correlated factors such as trends in crime statistics, gentrification, major commercial real estate purchases by new employers, and stock market indices. In addition, linear regressions for each region could identify potentially undervalued homes based on whether the ask price falls below the linear regression. 

#####Building for Scalability & Increased Complexity

Additional options and filters to view more cuts of the data, such as the ability to filter by number of bedrooms, baths, square footage and price level both for the heatmap and the active listing markers. In addition, users will have the option to view the choropleth map with regions broken out by increasing granularity, such as block groups. 

I realized from the project this is much more complex than it seems both in terms of managing how to structure the code and managing performance. As I noted earlier, as the number of permutations of options users can select grows, the less feasible it is to pre-calculate and store metrics for every scenario in the database. However, having the server run many calculations on the fly can significantly slow down the application. 

To solve this problem, I would experiment with a combination of techniques such as adopting PostGIS, creating a caching layer, using Tilemill to pre-style and serve my own tiles, decreasing the granularity of regional breakouts in the choropleth map at a higher zoom level, and restricting the data calculations within the specific user's viewport.  

On the front-end, I noticed that as more filter options are introduced, the complexity grows at an increasing rate as the number of conditional statements and edge cases increase. I would need to refactor my code so that variation is encoded as data and not as control and explore frameworks such as AngularJS. In terms of rendering, I would also explore a new technique called UTFGrids that can handle a large number of data objects on a map. 

#####Interactive Time Series Graphs

I'd like to create interactive time series line graphs that allow users to select multiple metrics and regions to compare on the same graph. 

