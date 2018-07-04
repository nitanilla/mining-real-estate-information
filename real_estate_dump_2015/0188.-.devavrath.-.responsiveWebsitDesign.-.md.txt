responsiveWebsitDesign
======================

Property search using Zillow &amp; Bootstrap, JQuery, and Facebook Mashup

This project allows users to search for real estate listings using the Zillow API 
(www.zillow.com) and the results will be displayed in a tabular format.
A PHP file to returns a JSON formatted data to the front-end and the front-end
(making asynchronous AJAX calls) will parse the JSON data and show it in a nicer-looking UI (using
Bootstrap JS). The PHP file is present in the devavrath/responsiveWebsitDesign/tree/master/HW8/WebContent/php 
directory and this can be hosted on any cloud platform.
A user can enter a property address in the format (street address, city, state) for looking up real
estate listings in Zillow if available. The state text-field should be a drop-down
list of all US states abbreviated in two letters (e.g., CA or IN).
The user should enter values for street address, city and state before clicking on
the Search button. Once the user clicks on the Search button, a layout with two tabs is returned.
The first tab contains the basic real estate information table that includes Property type, 
last sold date etc information. The tool also provides an additional feature of posting 
the returned information on facebook 
The second tab will display the Historical Zestimate charts of the searched
property. It needs to show three charts in a photo gallery.
