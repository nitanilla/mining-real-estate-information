# Real Estate Lister

An application that fetches & displays real estate listings from Mongo database. Enables a user to view and list properties, as well as search for properties that match given criteria. Deployed at https://real-estate-lister.herokuapp.com/.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

* [npm](https://www.npmjs.com/) - Package manager for JavaScript
* [Grunt](https://gruntjs.com/) - JavaScript task runner
* [Node.js](https://nodejs.org/en/) - JavaScript runtime
* [MongoDB](https://www.mongodb.com/) - Database used

### Installing

Download files

Install dependencies

```
$ npm install
```

Run Grunt in the root directory

```
$ grunt
```

Import listing data from the directory that contains ‘listingData.js’.

```
$ mongoimport --db realestate --collection listings --file listingData.js
```

Start a local server

```
$ npm start
```

Access the local installation via localhost.

## Deployment

Deployed using hosting by [Heroku](https://www.heroku.com/) and [mlab](https://mlab.com/).

## Built With

* [jQuery](https://jquery.com/) - Front-end JavaScript library
* [Node.js](https://nodejs.org/en/) - JavaScript runtime
* [Express](https://expressjs.com/) - Node.js framework
* [MongoDB](https://www.mongodb.com/) - Database used
* [Bootstrap](http://getbootstrap.com/) - Styling framework
* [npm](https://www.npmjs.com/) - Dependency management
* [Grunt](https://gruntjs.com/) - Task runner

## Author

* [**Anna Springfield**](https://github.com/aespringfield)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Thanks to the instructors at Prime Academy for inspiring this project
