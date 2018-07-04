# Smarta

## Introduction

AHAI(Andreea Uta, Huiqi Zhou, Amos Gichero, Ian Price) has engineered an application to connect Marta and local Atlanta businesses together. Our goal is to make Atlanta more accessible for Marta riders. Smarta links Yelp, Marta, and Google Maps together to easily search for businesses along your Marta route.

With Smarta you can search by routes or specific stops, and you can also select your preferred walking distance from the stop. You can filter the search by keywords, ratings, and prices. As our city grows we hope to see Marta expand, and applications like Smarta in higher demand. Marta is Smarta.

## Technologies We Used
* HTML
* CSS
* Node.js
* PostgreSQL

## Node Modules We Used
* express
* handlebars
* bluebird

## APIs We Used
* Google JavaScript API
* Yelp API
* Marta API

## Functionalities
1. You can search by key word, price, rating, walking distance to a Marta stop
![search page](./public/assets/search_page.png?raw=true "search page")
2. By putting in above filter and choosing a route and a stop, you can find businesses around that stop. The infowindow show you a picture and some basic information about the business. If you want to know more, you can go to the Yelp page
![search by stop](./public/assets/map_view_route.png?raw=true "search by stop")
3. Moreover, you can find businesses around the entire bus or train line
![search by route](./public/assets/map_view_stop.png?raw=true "search by route")
4. Beside the map view, you can also switch to table view
![table view](./public/assets/table_view.png?raw=true "table view")

## Challenges
1. We first decided to build a house finder app for Marta riders. But soon we found that Zillow API only provide information about specific addresses. It doesn't provide general search function. So we decided to switch gears to use Yelp API instead. But we still hope to find the real estate data to accomplish our original goal.
2. After we downloaded data files about Marta routes/trips/stops information, the only data combination of the stops and other ones are a one-million row file. When we were inserting the data to the database, node.js cannot handle reading that large of a file. We first tried to use a bash command "split" to split the txt file to about 100 small files. It took us a long time to insert the data, but we found that this bash command does not always break file at the end of a row, therefore caused some data parsing problems. We eventually decided to put the txt file in the server and directly run psql command to copy csv data into the database.
