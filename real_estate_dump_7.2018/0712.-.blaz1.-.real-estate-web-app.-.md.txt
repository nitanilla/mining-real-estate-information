# Real estate web app
#### Assignment description 
Implement a web application for real estate advertisement.  The application should provide services of buying, selling and renting real estates. Different categories of users will access the application: guests, users who post an advertisement, back-end users (like persons responsible for the verification of advertisements or super users).

Defining precise data model is left to students, but some of the data usually contained for real estates are: name, type, location, price, area, images …

Beside real estate data, each advertisement has its own attributes like identifier, publishing date, modification date, user who posted it, contact phone, email, comments …

Real estates are categorized into different categories like apartments, offices, land …

Registered users are either natural or legal persons. Within legal person (like real estate agency), specific natural person can be registered.

The application should support a rich and efficient search feature. Various search criteria should be defined like: transaction type (buy or rent), type, location, minimum and maximum price, minimum and maximum area … 

Since the location of a real estate is very important, the application should provide location information in an efficient way (probably using a geographic map). 

### Examples 
So far, different applications of this type have been developed. Some of the examples are 
- [Zillow](http://www.zillow.com/) – the biggest USA system for real estates
- [Nekretnine.rs](http://www.nekretnine.rs/) – a Serbian platform for real estate advertisements
- [Građanski oglasnik](http://www.gradjanskioglasnik.rs/) – a local real estate web site mostly used for the area of Novi Sad

### Implementation 
The system should be implemented as a client-server web application.

The server side should be implemented using Java technologies and Spring framework.

The client side should be implemented using JavaScript technologies and AngularJS framework.

The application should be tested using automated unit and end-to-end tests written in JUnit, Jasmine, Selenium and Protractor.