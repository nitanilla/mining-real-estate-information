## Restate - A real estate market analysis application

[Restate Live](https://andrewopes789.github.io/Restate/)

### Background and Overview

Restate is a general guide for everyone from first-time homebuyers to seasoned real estate investors, to gain a sense of the real estate
market in the areas they are interested in purchasing a property.

Users enter an initial zip code for which they would like market information, and then for the selected area, the application will map the
following analytics versus time:

* Average Price of All Listings
* Median Price of All Listings
* Count of Sold Listings

### Functionality & MVP

In Restate, users will be able to:

* Select an area to retrieve real estate analytics for
* Select which analytics parameters are mapped on the graph
* Specify the timeframe to receive analytics for, segmented by month, dating back to 2011

In addition, this project will include:

* An initial modal to select a zip code for the search
* An About modal describing the basic functionality

### Wireframes

![Initial modal](https://github.com/andrewopes789/restate/blob/master/wireframes/initial-modal.png)

![Graph render](https://github.com/andrewopes789/restate/blob/master/wireframes/main-page-render.png)

### Architecture and Technologies

This project will be implemented with the following technologies:

* Vanilla JavaScript for overall structure,
* `Chart.js` for the graph render,
* `Onboard API` for real-time real estate analytics,
* Webpack to bundle and serve up the various scripts.

In addition to the webpack entry file, there will be one script involved in this project:

`script.js`: this script will handle the logic for creating and updating the necessary filters for the graph.
`chart.js`: this script will handle the render for creating the graph.

### Implementation Timeline

#### Over the weekend:

* Familiarize myself with Chart.js and Onboard API

#### Day 1:
Get webpack up and running. Create `webpack.config.js` as well as `package.json.` Write a basic entry file and the bare bones
of the scripts outline above. Learn the basics of the API and how to fetch the data. Goals for the day:

* Get `webpack` serving files and frame out index.html
* Learn enough about the API to properly fetch data with the api key
* Learn about `Chart.js` and start framing it out.

#### Day 2:
Build out the scripts and the chart filters to change the path in response to user input. Goals for the day:

* Finish building out the relevant scripts
* Make the app make a new API call each time the user changes the location or date of his/her search

#### Day 3:
Connect the chart filters and the chart and have the chart be responsive in real-time to the user's selections. Goals for the day:

* Get the chart up to display all the paramaters fetched by the API call
* Get the chart to re-render in real time every time the user changes the parameters of the query
* Create the About modal

#### Day 4:
Style the frontend, making it polished and professional. Goals for the day:

* Style the initial city selection modal
* Style the graph and filters box
* Style the About modal

### Bonus Features
There are many directions in which this project could evolve.

* Retrieve and plot analytics for a specific property, including an automated fair market value
* Plot specific analytics for multiple areas at once
