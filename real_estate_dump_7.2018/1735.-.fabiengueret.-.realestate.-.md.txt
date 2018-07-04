# Real Estate General Pricing Model

## Objectives
General Project aiming at modelling prices for the real estate market according to location and type of property in the UK.

- The model detects property types and differentiate between them. 

- The model produces sensitivities to property features beyond the traditional characteristics (eg design or luxury level)

- The property owners or investors are be able to know what improvement to make

- The model links property asking prices with transanction prices and rental value

- The model is able to identify outlier for investment opportunities

## Project blocks

Project Divided in different blocks

### Trawling the existing real estate websites (rightmove and Zoopla)
RM_Super_Scraper.py
This scraper define a class for a specific search, return results as a dataframe and saves unique instances to an SQlite database (periodically). Data from RightMove.co.uk, postcode driven.

londonharvest.py 
This is a simple example of how to use the RM Super Scraper on the postcode of London, the search can be tweaked so as to search the last 3,7,14,infinite days, it can be an express search avoiding the time consuming OCR on floorplan. 

RM_RandomisedSamplingScraper.py
This scraper is nearly indentical to the Super Scraper but rather than go through all the page in a search result, returns the results from a simple page chosen randomly. Due to crash and time management we had issue we over representation of expensive properties posted recently. This redressed the selection bias.

### Data analysis and graph representations
univariate
bivariate
multivariate

### Regression / Prediction / Random Forest
- Data Analytics / Rental Yield
- Data Analytics / Offer Prices
- Data Analytics / realised prices

### Classification
Property Types: clustering

### Geo-localisation
Location and postcodes finder

### Soft features detection
- design quality
- age
- attractivity

