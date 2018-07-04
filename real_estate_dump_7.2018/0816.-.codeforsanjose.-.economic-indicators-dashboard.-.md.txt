Economic Indicators Dashboard 
===============================



[![Build Status](https://travis-ci.org/codeforsanjose/economic-indicators-dashboard.svg?branch=master)](https://travis-ci.org/codeforsanjose/economic-indicators-dashboard?branch=master)
[![dependencies](https://david-dm.org/codeforsanjose/economic-indicators-dashboard.svg)](https://david-dm.org/codeforsanjose/economic-indicators-dashboard)
[![devDependency Status](https://david-dm.org/codeforsanjose/economic-indicators-dashboard/dev-status.svg)](https://david-dm.org/codeforsanjose/economic-indicators-dashboard#info=devDependencies)
[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)

[![Stories in Ready](https://badge.waffle.io/codeforsanjose/economic-indicators-dashboard.svg?label=ready&title=Ready)](http://waffle.io/codeforsanjose/economic-indicators-dashboard)

See the [wiki](https://github.com/codeforsanjose/economic-indicators-dashboard/wiki) for additional notes on this project. 

[Initial mockup prototype](http://codeforsanjose.com/indicators)

## Table of contents

  * [Goals](#goals)
    * [10 Second Test](#10-second-test) 
  * [Target Audience](#target-audience)
    * [Usage Frequency](#usage-frequency) 
    * [Roles](#roles)
  * [Website Attributes](#website-attributes) 
   * [Related Sites](#related-sites)
   * [Data Sources](#data-sources)
   * [Example Sites](#example-sites)
  * [Minimum Viable Product](#data-sources)
  * [Stack](#stack)
   * [Getting Started](#getting-started)
     * [Publishing the site](#publishing-the-site) 
   * [Structure](#structure)
  * [Run local data](#run-local-data)

### Goals
1. Elected officials, policymakers, businesses, nonprofits and community members have access to an "at-a-glance" snapshot of how the San Jose economy is doing. 
2. City staff have a central, standard source of economic data for reporting and policymaking purposes. 
3. OED staff time spend less time servicing one-off data requests. 

#### How will progress toward goals be measured?
1. Use of dashboard in discussions about San Jose economy (Committee and Council meetings, public meetings, etc)
2. Reduction in number of individual data requests to OED staff
3. Site traffic analytics

#### 10 second test?  
In 10 seconds a user should be able to get a sense of whether the SJ economy is doing well or poorly. 

In 30 seconds a user should be able to find a specific statistic that he/she is looking for (or determine that it is not listed on the page). E.g. number of jobs in San Jose. 

#### Does this map to an existing city initiative?
Yes, ongoing data services provided by Office of Economic Development staff. 

### Target audience
* San Jose elected officials, policy makers and other local government staff
* Real estate developers, brokers and investors
* Nonprofit organizations that make advocate on specific policy issues (urbanism, housing, business climate)
* Journalists writing about San Jose
* Companies looking to relocate to San Jose
* People looking to live in San Jose
* Current San Jose residents

#### Usage Frequency
* As needed for reports, articles, etc (infrequently)
* Monthly Community and Economic Development Committee meetings
* Quarterly updates 

#### Roles
* Viewers
* Users of the data (e.g. journalists, analysts, researchers)
* Data entry (back-end)
* Developers

### Minimum Viable Product (MVP) description
* Static webpage showing key numbers for current quarter and change from previous year (no interactive charts)
* Look-and-feel is consistent with SJeconomy.com website (doesn't have to be perfect match, but passable)

### Website attributes
|Attributes  | Required |Notes |
| ------------- | ------------- |-----|
| Accessibility  | ||
| Device support  |   | Web, Mobile, Tablets (verify touch events), (not watches) |
| Browser support  |   | Chrome, Firefox, Safari, IE (IE 10+)|
| Languages  |   |Current site supports many languages|
| Analytics  |   ||


#### Related Sites
[San Jose Office of Economic Development](http://sjeconomy.com/) website done in Wordpress

#### Example sites
[Denver's economic indicators](http://www.metrodenver.org/research-reports/monthly-economic-indicators/)

[San Diego's economic dashboard](http://www.sandiegobusiness.org/research/dashboard)

[California Center for Jobs & the Economy](http://www.centerforjobs.org/data-tool/#santa_clara)

[Boston's transportation agency performance dashboard](http://www.mbtabackontrack.com/performance/index.html#/home)

[Montgomery County's dashboard](https://reports.data.montgomerycountymd.gov/countystat/objective/economy)


##### Release targets
* Share alpha version with Office of Economic Development staff in April/May
* Launch beta version to San Jose elected officials at June 27, 2016 Community and Economic Development Committee meeting 
*
#### Longer term vision for site
TBD

#### Integrations
(List any existing city or external systems that should be integrated with this site.)
Ideally the indicators would be populated from the [City of San Jose's open data portal](http://data.sanjoseca.gov/home)

#### Standards
[ISO 37120](http://www.iso.org/iso/catalogue_detail?csnumber=62436) - Not widely adopted yet.
  * [ISO 37120 Data Portal](http://open.dataforcities.org/) - Select Data Portal menu

### Stack
See the package.json for the full set of libraries/tools used

#### Front end
* React - https://facebook.github.io/react/
  * All styles are set and maintained in external files. All tags, classnames, ids are set in jsx. 
* React-redux - http://redux.js.org/
* scss - http://sass-lang.com/
* Bootstrap - http://getbootstrap.com/
* nvd3 - http://nvd3.org/
  * D3 - https://d3js.org/

#### Server  
The server is simply for development to support hot module replacement
* Koa - http://koajs.com/

#### Backend
Currently there is not a backend.  In the future if one needs to be created, node will be used so that code can be shared between the front and back ends.

#### Build
If there are any eslint errors, the build will fail.

* npm - https://www.npmjs.com/
* better-npm-run - https://www.npmjs.com/package/better-npm-run
* babel - https://babeljs.io/
* webpack - https://webpack.github.io/
* travis (github integration) - https://travis-ci.org/

###### Quality checks
* eslint - http://eslint.org/ 
  * Uses the standard rules (http://standardjs.com/rules.html) via https://www.npmjs.com/package/eslint-config-standard
* phantomjs - http://phantomjs.org/
* sinon - http://sinonjs.org/
* chai - http://chaijs.com/
* codecov - https://codecov.io/
* karma - https://karma-runner.github.io/0.13/index.html

#### Getting started

The project uses the [react-reduct-starter-kit](https://github.com/davezuko/react-redux-starter-kit) by [Dave Zukowski](https://github.com/davezuko).   

This has been run on mac and linux oses.

Prerequisites

[Installer for node.js and npm ](https://nodejs.org/en/)
* Node.js - Verified with 4.x, and 6.x - Currently node is used for the build process and development server
* npm - node package manager.

Just clone the repo and install the necessary node modules:

```shell
$ git clone https://github.com/codeforsanjose/economic-indicators-dashboard.git
$ cd economic-indicators-dashboard.git
$ npm install                   # Install Node modules listed in ./package.json (may take a while the first time)
$ npm start                     # Compile and launch
```
##### Publishing the Site
To deploy to gh-pages

Note:  data is temporarily hosted on gh-pages and will eventually be hosted at a location TBD

```shell
# In the economic-indicators-dashboard folder, run the following
$ npm clean                               # Remove the dist folder which contains the compiled pieces
$ npm run deploy                          # Generate a clean build in the dist folder

# Clone the gh-pages branch into a different folder (e.g. branches folder)
$ git clone -b gh-pages https://github.com/codeforsanjose/economic-indicators-dashboard.git 
$ cd economic-indicators-dashboard        # cd into the gh-branches version of economic-indicators-dashboard
$ git rm *.js *.css                       # remove the previous bundles of the css and js

# copy the bundled *.js, *.css and index.html and about.html from the dist folder to the gh-branches folder
# The text at the top of the indicators page may have a link to the about.html.  This text is coming from data/general_config.json hosted on gh-pages.  The path to the about.html may also need to be updated

# add, commit & push the changes to the gh-pages branch
$ git add *.js *.css *.html                               # Add any other files that changed (e.g. new image files, etc.)
$ git commit -m "substitute your checkin message here"    # Commit the files 
$ git push                                                # push the files to github

# Verify the site
# In a browser window, browse to the url [http://codeforsanjose.github.io/economic-indicators-dashboard/](http://codeforsanjose.github.io/economic-indicators-dashboard)
```
Great, now that introductions have been made here's everything in full detail:

|Script|Description|
|---|---|
|`npm start`|Spins up Koa server to serve your app at `localhost:3000`. HMR will be enabled in development.|
|`npm run compile`|Compiles the application to disk (`~/dist` by default).|
|`npm run dev`|Same as `npm start`, but enables nodemon to automatically restart the server when server-related code is changed.|
|`npm run dev:nw`|Same as `npm run dev`, but opens the redux devtools in a new window.|
|`npm run dev:no-debug`|Same as `npm run dev` but disables redux devtools.|
|`npm run test`|Runs unit tests with Karma and generates a coverage report.|
|`npm run test:dev`|Runs Karma and watches for changes to re-run tests; does not generate coverage reports.|
|`npm run deploy`|Runs linter, tests, and then, on success, compiles your application to disk.|
|`npm run flow:check`|Analyzes the project for type errors.|
|`npm run lint`|Lint all `.js` files.|
|`npm run lint:fix`|Lint and fix all `.js` files. [Read more on this](http://eslint.org/docs/user-guide/command-line-interface.html#fix).|

**NOTE:** Deploying to a specific environment? Make sure to specify your target `NODE_ENV` so webpack will use the correct configuration. For example: `NODE_ENV=production npm run compile` will compile your application with `~/build/webpack/_production.js`.

#### Structure

```
.
├── bin                      # Build/Start scripts
├── build                    # All build-related configuration
│   └── webpack              # Environment-specific configuration files for webpack
├── config                   # Project configuration settings
├── coverage                 # Test coverage results - NOT CHECKED IN
├── dist                     # Files to deploy - NOT CHECKED IN
├── interfaces               # Type declarations for Flow
├── node_modules             # Results from npm install - NOT CHECKED IN
├── server                   # Koa application (uses webpack middleware)
│   └── main.js              # Server application entry point
├── src                      # Application source code
│   |   ├── client
│   |   |   ├── server       # Koa application (uses webpack middleware)
│   |   |   |   └── main.js  # Server application entry point
│   |   |   ├── app
│   |   |   |   ├── charts       # nvd3 pieces
│   |   |   |   ├── components   # Generic React Components (generally Dumb components)
│   |   |   |   ├── config       # Constants, urls pieces
│   |   |   |   ├── containers   # Components that provide context (e.g. Redux Provider)
│   |   |   |   ├── layouts      # Components that dictate major page structure
│   |   |   |   ├── redux        # Redux-specific pieces
│   |   |   |   │   ├── modules  # Collections of reducers/constants/actions
│   |   |   |   │   └── utils    # Redux-specific helpers
│   |   |   |   ├── routes       # Application route definitions
│   |   |   |   ├── static       # Static assets (not imported anywhere in source code)
│   |   |   |   ├── styles       # Application-wide styles (generally settings)
│   |   |   |   ├── views        # Components that live at a route
│   |   |   |   ├── index.html   # index.html
│   |   |   |   └── main.js      # Application bootstrap and rendering
└── tests                    # Unit tests
```

### Run Local Data

This will provide an overview of running the application using local data.   

###_Remember to restore that settings that apply to the production settings if you are deploying the configurations_

We will be using two simple data servers.  One for the configuration data and second one for the indicator data.   This was tested using http-server which can be downloaded from npm:  https://www.npmjs.com/package/http-server

The three servers that will be running are:

* Dashboard:  http://localhost:3000/local.html
* Configuration: http://localhost:8080
* Data: http://localhost:1234

The references to these are as following:

* src/local.html - This is the entry point for the dashboard.  Enter in the url for the configuration on the following line

```
    <div id='root'  data-config='http://127.0.0.1:8080/general_config.json'></div>
```

* demoData/dashboard2/config/general_config.json - This overrides the default urls that currently point to SJ github repo for the configuration and the opendata portal for the data.

Confirm that the following settings are in the general_config.json - see snippet below

   "useURLConfig": true,
   "configURL": "http://127.0.0.1:8080",
   "dataURL": "http://127.0.0.1:1234",
   
Verify the json formatting by pasting the contents of the file into an online JSON format verifier.  An example can be found here:  http://jsonlint.com/

```
"urlConfig": {
   "useURLConfig": true,
   "configURL": "http://127.0.0.1:8080",
   "dataURL": "http://127.0.0.1:1234",
   "useDataMap": true,
   "dataMap": {
      "SAN-JOSE-ECONO-INDIC":"econ_indicators_q12016_junar_CMO-T17-117LT_1.csv",
      "MONTH-JOBS-TOTAL" : "monthly_jobs_june2015.csv",
      "SAN-JOSE-JOBS-BY-SECTO" : "monthly_jobs_by_sector_june2015.csv",
      "MONTH-UNEMP-RATE": "monthly_unemployment_may2016_sj_sjmsa.csv",
      "LABOR-FORCE-BY-AGE": "labor_force_by_age_acs2014.csv",
      "EDUCA-ATTAI-FOR-SAN-JOSE":  "edu_attainment_2014.csv",
      "MONTH-APART-RENTS": "monthly_apt_rend_rendjungle.csv",
      "MEDIA-HOME-PRICE": "monthly_home_prices.csv"
   }
  ```
  
The dataMap maps the OpenData portal guid to the corresponding csv file that was downloaded.

#### Steps to run

```
cd [cloned repo directory]/demoData/dashboard2/config
http-server --cors

cd [cloned repo directory]/demoData/dashboard2/data/q1
http-server --cors -p 1234

cd <cloned repo directory>
npm start

# In your browser, navigate to 'http://localhost:3000/local.html'


```
