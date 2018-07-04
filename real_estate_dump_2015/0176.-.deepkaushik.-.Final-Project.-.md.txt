
# Final-Project 

NYC Real Estate App

Our app is designed to display real estate listings in the New York City area. It a open source and was written for the NYU School of Professional Studies Android course NYU INFO1-CE9416, taught by Mark Meretzky,

This application is divided into six different screens and accessable through menu bar [+] sign located at right corner of each screen. User can use these following screens:

1. LAUNCH SCREEN displays a list of latest real state news articles. We're useing static feeds through parse.com.

2. MAP SCREEN - Use can access Maps page from menu button. At the top is an address text field and a search button. Below is a map containing blue markers indicating apartments for sale in New York City. Clicking on each listing will display specifics about that listing from a parse.com database, displayed in an pop-up window. The pop up window also queries a StreetEasy API to get aggregate real estate statistics like average price, average square footage, and average number of weeks on market for all the apartments with that number of bedrooms in that zip code. User can enter an address and click the search button to add a red marker to the map below at the address listed. 

3. SAVE LISTING screen is used to edit data for a new real estate listing. User can enter data such as a description, price, square footage, and number of bedrooms. All details save and uploade to a parse.com database.

4. FILTER LISTING screen allows user to filter map results by the number of bedrooms and by the maximum price of the listing.

5. MAP SETTING allow user to control the style of the google map (normal, hybrid, satellite and terrain) and the angle of the camera.

6. GOOGLE VOICE SCREEN allow user to use google speeach API to enter address rather then typing address into map edit field.

Future of the app: 
Currently anyone running the app can post and edit real estate listings without login. In next update user have to login into app before save there search results. Also we would like to add more information for each real estate listing, like contact person, telephone and e-mail address.

Good to Know:

1. For context menu we used a third party, Yalantis libraries that makes android user interface objects. (find repository here: https://github.com/Yalantis/Context-Menu.Android)
2. To get permission to access Google Maps in this application you will need to register with Google and enter your own API key in the google_maps_api.xml file in the values folder.

Project Timeline:

1. Kick off meeting and requirements - 4 hours
2. Outlining application and researching API’s and source of data - 6 hours
3. Design and Programming application - 35 hours
4. Debugging application - 15 hours
5.  Documenting application - 3 hours

Last but not the least, we're kindly thankful to Mark Meretzky for showing us details and useful examples that made learning easy and all our classmades for their full support.

Thanks,

Team Android

Asa and Deepali

