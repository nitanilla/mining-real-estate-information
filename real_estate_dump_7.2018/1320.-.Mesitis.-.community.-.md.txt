## Canopy Developer Community Page
*Sample code and all things community*

[Canopy](https:/canopy.cloud) is a data aggregation and analytics platform. We are currently targeting the high networth client segment, however the data structure is flexible enough to handle all uses ranging from personal finance management for a mass affluent user all the way to risk managing a derivative trading book at a bank. 

High Networth clients have complex holdings. These holdings are spread over financial (e.g. bonds and equities) and non-financial (e.g. real estate and art) assets all over the world with multiple custodians. Data about these holdings is available in various non standard formats ranging from proper data feeds and PDF statements all the way down to Excel sheets and hand written notes.

Our mission statement is to help aggregate this data (irrespective of data source), store them in a standardized format, check everyday for data consistency and provide a (usually daily) mark-to-market. This data is then available via Open APIs for all sorts of use cases ranging from simply tabulation and doing your taxes to complex analytics / trade suitability checks / trade suggestions / digital advice / performance reporting and benchmarking etc.

Canopy currently offers a turnkey service where we collect and upload your data from multiple sources and ensure data consistency. We also provide a browser based front end, an Excel Front End, Open APIs, PDF and Ppt Report Generators, Emailing programs etc. etc. 

However we are very open to people who want to build other (or competing) apps / products on our platform. This page is meant for people who are looking to develop applications on our platform and contains sample code and descriptions of APIs. 

There are already a few apps in the AppStore (Excel Front End and an Analytics App)

Please email us for further information (including if you want a demo login)

### Canopy Universal Language (CanopyUL):
[CanopyUL](https://mesitis.atlassian.net/wiki/display/HOW/Canopy+Universal+Language) is a open source format designed for non-coders (who are more familiar with Excel than with JSONs) to freely transfer information about an accounts transactions and holdings across banks and custodians


### Canopy Open APIs
All (well almost all !!) data inside Canopy can be accessed via APIs ... a Postman description page of these APIs is [here](https://documenter.getpostman.com/view/884147/canopy-api-calls/6YtywA3)

### Canopy Analytics App
An analytics server that pulls a particular users data from Canopy (via APIs - requires regular authentication to access the data being downloaded) and does a large number of analytics on it. Accessible via Open APIs .. sample [here](https://documenter.getpostman.com/view/884147/canopy-midapi-calls/6YwzFUx) 

### Microsoft Excel Front End
For users who want to access the data directly via Microsoft Excel. This spreadsheet uses the same authentication for the Open APIs (i.e. you need to enter your username / password and OTP (if activated). It works on both Windows and Mac and does not require any particular add-ins to be installed (although it works a little faster on Windows)
Always look for the latest version (as earlier versions may not work).

The Excel Front End calls both the Canopy Open APIs as well as the Canopy Analytics App as required.  

### MIT License
While Canopy itself is not open source, we encourage developers to build applications on top of Canopy. Therefore all code in this repository is provided under MIT license
