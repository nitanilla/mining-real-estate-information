# Bizzey Real Estate - Real Estate Assignment Example

Bizzey Real Estate is a demonstration of a real estate style website intended to display my progress at  Prime Academy through week four in the journey towards becoming a full stack application developer.

Given a list of existing properties (located in `listingData.js`), our cohort was tasked with creating a full stack application that would display the data and use CRUD routes to change what data is being displayed.  The 'pro mode' of the assignment required us to deploy the site to Heroku with the database hosted on mLab.

## Assignment

_Assignment provided for reference and to provide project inspiration for new developers_

### Base Mode

* Create a Full Stack application from the ground up using jQuery, Node, and MongoDB

* Work with the data set that we provide for you

* Use Bootstrap to present the data

* Account for the different data (“rent” versus “cost) and ensure that this is noted on the display of the information, by listing “For Rent” or “For Sale” based on which of the two properties that it has.

### Hard Mode

* Create an interface for adding additional properties to the collection. You will need to give the user an option for either a Rent property or a Sale property.

### Pro Mode

* Host the application on Heroku and mLabs. 

## Getting Started

Follow the steps below to get a copy of the Bizzey Real Estate application up and running on your local machine.

### Prerequisites

* Git
* Grunt  
* MongoDB  
* Node and NPM  
* RoboMongo (or a similar MongoDB management tool)  

### Installing

* Git
  * Initialize a Git repository
  * Add the remote
  * Pull the project to your local repository
```
>git init
>git remote add origin https://github.com/gnargnor/bizzey-real-estate.git
>git pull origin master
```
* Grunt  
  * Start Grunt 
```
>grunt
```
* MongoDB  
  * Start a local MongoDB database server on port 27017
  * Replace the MongoURI in `app.js` with the local MongoDB server
```
>Mongod
```
```
//var mongoURI = "mongodb://username:password@host.com";
var mongoURI = "mongodb://localhost:27017" - for use on local machines
```
* Node and NPM  
  * Install dependencies
  * Spin up the Node server
```
>npm install
>npm start
```
* Browser  
  * Navigate to `localhost:5000`

#### You'll be directed to MEAN MUD's login page.  Select "register" to register a new user and get started.

## Built With

* [Node.js](https://nodejs.org)
* [Express](http://expressjs.com/)
* [jQuery](jquery.com)
* [MongoDB](https://mongodb.com)
* [Mongoose](http://mongoosejs.com)
* [Bootstrap 3](http://getbootstrap.com/)
* [Heroku](http://heroku.com)
* [mLab](https://mlab.com)
* CSS3
* HTML5
* JavaScript

## Author

* **Logan Kelly** - *Initial work* -  
  * [github.com/gnargnor](https://github.com/gnargnor)  
  * [Bizzey Tech, LLC](http://www.bizzeytech.com)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments


* [Prime Academy](http://www.primeacademy.io) - assignment credit
