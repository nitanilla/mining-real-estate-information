# jmse-test
Test application for jm.se

# Given Test assignment: 
Create a lightweight Django or Flask app that scrapes data from this website: www.jm.se and displays real 
estate objects in Stockholm in a list. Information that needs to be displayed: 
title of the project, status(planned, selling, sold etc), area of the project, 
URL to the project on jm.se website, image of the project. 
Use Python library Scrapy or another tool of choice for web scraping. 

# How as I understood this:
1. Source of info - website www.jm.se. Real estate objects in Stockholm placed in this url: http://www.jm.se/bostader/sok-bostad/#c=stockholm&tab=objects&listmode=box
2. Information must be taken from this source and show in easy way on created app
3. Must be shown 3 field, Image and link for real page on the site.
4. Image must be stored in app (not external link).
5. Due to work can be used web scaping tool

# How it was realised:
1. Django
2. Info on the original site preparing dynamically using JavaScript. 
 Not so many ways to get such kind of information without using client browser. I decided not to use Scrapy 
 or similar tool because of significant overhead. Just use an AJAX calls.
3. All import done through management command ./manage.py grab It can be used in cron-like systems too.
4. Import routine try to get change status of Estate objects if it changed and hide objects, that found 
 missed during next start of import.
5. Output paginated by 21 items (by 3 in row).

   
