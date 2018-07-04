## Cortlandt

Are you tired of manually going through several real estate and aggregator websites? Even once you set your search parameters, you must be sick of opening a billion different tabs to check how long your new commute would be, what are the (sports) facilities in the area. 

I was sick of that, hence this python script to regularly scrape and update information about relevant flats. Use rightmove to draw several search maps, saved them in the ```run.py```. It scrapes and saves results to a google sheet. 

Run it as a cron-job, which spins up a Docker container to regularly upload new flats and update old ones.

**Still work in progress - use at own risk**

### Requirements

  * Google sheet for results
  * Docker - I run this as a container
  * APIs: googlemaps, pysheets, selenium from pip
  * Keys to GoogleMaps and Google Sheets
  * phantomjs 


### Run

  * Save your credits and API keys to the json file with the following names. (delete .example from the filename)
     * g\_maps\_creds.json.example
     * service\_creds.json.example
     * g\_sheets\_id.json.example

  * Build and run a docker container - see Makefile
      * run.py takes 2 arguments - number of bedrooms and max monthly rent. Edit the Makefile run command to change defaults.

### Design

The Rightmove search URL keeps all necessary parameters, including the location identifier (as a set of polylines). This combined with Rightmove's scrape-friendly robots.txt makes it a good target for scraping. Having nanually selected and saved the search URLs for areas of interest, the programme takes number of bedrooms and monthly rent as arguments, inserts them into search URLs and scrapes new flats. 

sheets.py has the WSheet class, which holds the API sign in logic and wrappers around the pygsheets API.

directions.py - DirectionsFromFlat and coord\_tuple\_to_str method. Each scraped flat's coordinates is used to instantiate a new DirectionsFromFlat object. DirectionsFromFlat exposes get\_directions(), which returns a dictionary of results for the given flat. The \_find\_closest\_pool() includes different pools coordinates in its scope, but can override them with another dictionary of swimming pools in the format (name: coordinate\_tuple). 

scrape.py - FlatScrape object and separate get\_list\_of_flats method. The class and method each have a separate instance of phantomjs webdriver.

run.py:

  * parse CLI args - number of bedrooms and monthly rent
  * prepare search URLs with the given args
  * Get a list of flats already saved in the sheet
  * If new flat URL can be scraped, enrich its data with information on directions
  * Upload new flat to google sheets
  * Update old flats
  

#### Name

Named after the housing project designed by Howard Roark.

#### Thanks

[Stefano](https://github.com/roastario) idea and advice.
