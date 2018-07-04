#City Fighter
City Fighter is an interactive app that lets prospective web developers research
relevant information about major U.S. cities. City Fighter can display useful information
pertaining to web developers for the different cities, such as average salary,
number of current open job listings, local companies that are currently hiring web developers, cost of living, and even lifestyle-related concerns such as bike share information, weather, and real-estate prices.

#Getting Started
To get a copy of the app running on your local machine, check out the project repository on Github at https://github.com/Briik/Project3 and clone the json_backend_concept branch(it's the default branch).  For this to work please first run 'npm install' to get the necessary dependencies.  Make sure to then seed the data by running 'node seed.js'.  Next run 'nodemon' and go to localhost:4000 in your browser.

To run the app locally you will also need to create the env.js file, which has the following code (obviously you need to provide your own API keys):

module.exports = {
  PORT: 4000,
  MONGO_SERVER: 'mongodb://localhost/city_fighter',
  WUNDERGROUND_KEY: '',
  GLASSDOOR_PARTNER_ID: '',
  GLASSDOOR_KEY: '',
  INDEED_PUB_ID: '',
  ZILLOW_KEY: '',
  TRULIA_KEY: ''
}

#Unsolved Problems/Areas for development
We would like to make the front end more modular.  We also would add more complete front-end design.

#Hosted app
http://cityfighter.herokuapp.com/

#Built With
- mongodb
- express.js
- node.js
- jQuery
- HTML5
- CSS3

#Modules
- "bcrypt-nodejs"
- "body-parser"
- "dateformat"
- "connect"
- "connect-flash"
- "cookie-parser"
- "ejs"
- "express"
- "express-ejs-layouts"
- "express-session"
- "hbs"
- "mongoose"
- "request"
- "xml2js"
- "method-override"
- "mongodb"
- "morgan"
- "passport"
- "passport-local"

#Authors
- James Moon
- Daniel Alexander
- Bryce Lively

#License
This project is licensed under the MIT License.

#Acknowledgements
The authors would like to thank our instructors at General Assembly for guidance and help during the course of this project.  We would especially like to thank Nick Olds.
