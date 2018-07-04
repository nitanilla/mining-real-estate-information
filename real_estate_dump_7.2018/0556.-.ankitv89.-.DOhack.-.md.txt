#Find Me This!
##This project is no longer maintained!

A Google Maps based listing web app to help people share resources. WONT WORK IN CHROME AS IT NEEDS HTTPS FOR GMAPS.

The Project was created as a part of DigitalOcean India Hackathon in 24 Hours.

The Webapp is based on Google Maps. People can list the things they have in excess for sharing, lending or even selling. 

The inspiration was to help people in the situations like when they need something very urgently like a laptop charger or 
mobile charger or may be extra notebooks etc.

The search radius is limited to 15km such as to keep the idea of getting the required things now. The platform is fully adaptable to any requirement like real estate, food,or other services.

The Code used Google Maps geolocator to get the users location and used Geographical formula to calculate the distance between the listed item and his/her present location. This bypasses the need for using GMaps Distance Matrix APIs which has limitations in free plan.

##Development Platform Use: 
MeteorJS 1.3.3

##Directions for Use:
1) Run the App
2) Log in using password
3) Click Submit and fill in the form to list the items or search the home page to find the items. The phone number and address is listed out for the available items.

##Installations Instructions:

Please use this package for installation: https://github.com/arunoda/meteor-up/tree/mupx 

To run on local machine- Download and MeteorJS from meteor.com . Clone the repository, then type 'meteor' inside the project directory. It will download the necessary packages and run on localhost:3000 .  

