---
output: html_document
---
# shiny-apps
Building apps using shiny is really fun and easy so this repo is dedicated to various apps I built using the shiny package.

The following apps are now deployed:

* eximbank: https://umdocc.shinyapps.io/eximbank
mobile app for Vietnamese local bank. The app make use of R web crawling capability and MySQL. 

* estate: https://umdocc.shinyapps.io/estate
database project for real estate in Australia. The app aims to build a comprehensive database for house pricing and information in Australia by using data collected from various public sources. Shiny GUI provide some interactive and graphical information for the end users. Database uses the same RMySQL workaround for shiny apps.

* carsmpg: https://umdocc.shinyapps.io/project
This app uses data from the US Department of Energy to measure how a car manufacturer improves their MPG towards smaller engine size. The app will the grade a manufacturer based on how progressive this trend is.

* thedress: https://umdocc.shinyapps.io/thedress/
A small app for people to vote on the controversial dress. As shinyapps.io does not allow data update between sessions, data are stored using MySQL on my personal host.