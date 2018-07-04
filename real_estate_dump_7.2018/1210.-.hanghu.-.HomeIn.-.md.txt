##HomeIn

----

<img src="doc/HomeIn.png">

HomeIn provides an analysis tool for  housing data, prices, and crime rates on a multiple-layered map interface.  This visualization technology allows users to pinpoint areas and analyze their specifications and statistics before making a decision on a home purchase.

With HomeIn, users will have  access to past sales and crime data.  This repository is intended to exist as both a place where home-buyers can compare their house price to others in the area, and also as a tool that GitHub users can edit and create similar maps for themselves.

----

### Necessary Packages and License Information

All of the necessary implementations in this repository can be carried out using the following software.  All software is open source.

####Python packages:

- NumPy 1.11.1  
- pandas 0.19.1  
- matplotlib 1.5.3  
- geopy 1.11.0  
- folium 0.2.1  
- Pillow 3.0.0  

####Installing Packages:

**1. Install numpy, pandas, and matplotlib:**  
$ conda install numpy pandas matplotlib

**2. Install geopy:**  
$ pip install geopy

**3. Install folium:**  
$ pip install folium

**4. Install Pillow:**  
$ pip install Pillow

####Licensing info:

HomeIn uses the MIT license.  The data and packages used are completely open source.  We want to make  our code readily available  to be improved and utilized with suggestions and implemenations by our user base.  It is important the house photos are able to be edited, as they will not always provide a 100% accurate photo.  The MIT license for this project is descrived in full in **LICENSE.txt**.

----

###Directory Summary

**Data:** All data used in analyses is accesible from the data folder.  The data is described in full in the DATA_DESCRIPTION.md document.

**Examples:** This folder contains iPython Notebook walkthroughs of how we cleaned up our data as well as basic examples of how to use each python package.  A demo of a final map is also included.

**HomeIn:** All python modules used in the project directory are found in this folder.  Unit tests are also included for testable modules.

**doc:** Documentation for the project is found in this folder.  This includes the project summary, HomeIn logo, and walkthroughs on how to make a map.

**UsercaseExplication.md:** Use cases and scientific questions answered by the project.

**License.txt:** The  MIT license used for this project.  We thought that having open access to the data was important for multiple user bases. (i.e. real estate professionals, potential homeowners, etc.)

----

###Directory Structure

The package is organized as follows:

    HomeIn (master)  
    |---Data  
        |---King_County_Sheriff_s_Office.csv  
        |---cleaned_crime_data.csv  
        |---crime_info.csv  
        |---crime_info_sample_of_10.csv  
        |---house_crime_data.csv  
        |---kc_house_data.csv  
        |---merged_data_sample.csv  
        |---zipcode_king_county.geojson  
    |---Examples  
        |---Correlations.ipynb  
        |---FoliumExpl.ipynb  
        |---Geopy.ipynb  
        |---House_photos.ipynb  
        |---Map.html  
        |---Zipcodes.ipynb  
        |---crime_info_usage.ipynb  
        |---data_preprocessing.ipynb  
        |---layer_map.ipynb  
    |---HomeIn  
        |---__init__.py  
        |---crime_info.py  
        |---house_cluster.py  
        |---map_demo.py  
        |---test_zipcodes.py  
        |---unittest_crime_info.py  
        |---zipcodes_search.py  
    |---doc
        |---CSE599_project_summary.pptx  
        |---HomeIn.png  
        |---Makefile  
    |--.gitignore  
    |--DATA_DESCRIPTION.md  
    |--LICENSE.txt  
    |--README.md  
    |--UsercaseExplication.md  
    |--setup.py  

----

###Tutorial For Generating An Interactive Map With Custom Parameters

####Step 1: Download the Data

The raw datasets are all open data from [Kaggle](https://www.kaggle.com/harlfoxem/housesalesprediction) or [King County Open Data](https://moto.data.socrata.com/dataset/King-County-Sheriff-s-Office/4h35-4mtu). The main columns of the data are the GPS coordinates of the house and crime incidents, crime type as well as house information including price, _etc._ The data used to generate the demo Map are described in detail in **DATA_DESCRIPTION.md**

####Step 2: Geocode Crime Data and Merge with House Data

With the questions mostly concerning the users, the crime information around houses in the past a few years within the cutoff distance are generated and added to house data by three steps. The example in our case is in '/Examples/data_preprocessing.ipynb'.  

- **1. Set a year range.** In our case, we set the year range as the past 5 years before those houses are sold and drop all the crime data which are not in that time range.  

- **2. Set a cutoff distance.** The cutoff distance in our case is default as 1.0 mile. Plug in the gps corrdinates, house ids and crime type by the function _crime_info_output_ in module _crime_info_. This process might take a long time, in our case, it took 6.5h to generate all the crime data.  

- **3. Merge** the crime data with house data based on their ids.  

####Step 3: Obtain Google Maps API Key and Define URL Parameters

Google Maps API is used to acquire street view photos of the houses by longitude/latitude GPS coordinates.To use Google Maps API, inividual needs to apply for a key which allows 25000 free inquiries per key per day. Extra inquiries will be charged. 

- **1. Apply for a Google Maps API key.** Go to [website](https://developers.google.com/maps/documentation/javascript/get-api-key). Fill your personal information and acquire the key.

- **2. Define URL parameters.** In Google Maps API, static street view photos are defined with URL parameters in HTTP requests. The parameters include:
  - Location (latitude, longitude)
  - Size of image
  - user key
  - Compass heading of camera
  - FOV
  - Pitch (angle of camera in degrees).
  With all parameters defined in the URL, the HTTP request will return a image. Example: https://maps.googleapis.com/maps/api/streetview?size=300x300&location=-47.33,122.00&pitch=10&key=USERKEY (open this URL in browser).


####Step 4: Create Marker Popups

Marker popups are used to show information on each house. By default, it will show street view photo, house price and specifications, number of crimes in its neighborhood during the past 5 years. 

- **1. Present each house as a marker on map.** Location of the marker is determined by longitute/latitute GPS coordinates. The logo for marker can be customized. At this stage, such customization can only be done in source code [house_cluster.py](https://github.com/hanghu/HomeIn/blob/master/HomeIn/house_cluster.py).

- **2. Popups.** Popups appear after user click on the marker and contain house-related information. The information in the popup can be customized. However, at this stage, such customization can only be done in source code [house_cluster.py](https://github.com/hanghu/HomeIn/blob/master/HomeIn/house_cluster.py).

####Step 5: Create Map Layers and View Toggler

3 different layers of map is generated with view toggler.The example for our case is in '/Examples/layer_map.ipynb '.  

- **1. House marker cluster layer.** Each marker represents a house in our data set with image of the house from Google Maps API, information of house properties (price, living sqft etc.) and crime info for the past 5 years. The layer is generated using folium.MarkerCluster with personalized Popups.

- **2. Zipcode vs. House Price layer.** Choropleth map shows average house price in each zipcode. The layer is generated using folium.Map.choropleth. Addtional interactive funtion is applied to popup average house price when clicking each zipcode. This is done by changing the source code in folium. 

- **3. Crime heatmap layer.** Heatmap shows the incidence of crime for the past 5 years. The incidence of crime increases with the color change of heatmap (blue --> green --> yellow --> red). The layer is generated using folium.plugins.HeatMap.

- **4. Combination of multiple layers.** This can simply be done using folium.LayerControl().

----

### Tutorial For Operating Map Demo

The demo map can be found in '/Examples/Map.html'. Or use this [link](https://cdn.rawgit.com/hanghu/HomeIn/master/Examples/Map.html) to open the map in browser. The map contains 3 layers: house marker cluster layer, zipcode choropleth layer and crime heatmap layer. Use the view toggler on the top right corner of the map to display specific layers.

----
<img src="doc/Layers.png">
----

For the marker clusters, click each number cluster to zoom in until a single popup appears. Click this popup to show the house image, house info and crime info.
For the zipcode choropleth, click each zipcode to zoom in and center the region of your interest. This also provides an popup showing the average house price in this zip code

----
<img src="doc/Popups.png">
----
