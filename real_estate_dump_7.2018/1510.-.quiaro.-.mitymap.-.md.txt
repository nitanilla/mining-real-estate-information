Mity Map
=====================

Map crawler and property finder.

Find real estate listings in Costa Rica for properties on sale by their owners located in condominium complexes or gated communities.

---

## Features
- Find real estate properties listed as lots, houses or apartments.
- Filter listings by location, price and area.
- Tweaking the property filters immediately updates the number of relevant results.
- View all listings matching the search criteria in a table and showing location on the map -the map zooms and adjusts to fit all real estate listings.
- Sort search results by name, price or area.
- Select a property (on the table or the map) to view additional information on the property.
- Quickly find the location of a property on the map by making its marker stand out with an animation.
- Responsive design suitable for use in desktops, tablets and smartphones.

---

## Setup & Build

Follow these steps to get this project set up and running locally:

1. Clone the repository
```
$ git clone https://github.com/quiaro/mitymap
```

2. Go to the project directory
```
$ cd mitymap
```

3. Install the project dependencies
```
$ npm install
```

4. Build the project with [GULP](http://gulpjs.com/)
```
$ gulp build
```
This creates a `dist` folder where assets will be obfuscated and minified to be delivered to production.

Alternatively, you can also run `$ gulp` which builds the project and additionally starts a development server for quickly testing changes to the code.

---

## Technologies & Credits

This project consists of a client app built mainly with the Javascript Framework, [Knockout](http://knockoutjs.com/) and a trimmed version of [Materialize](http://materializecss.com/), a responsive front-end framework based on Material Design. For data, this app combines static data loaded from a JSON module with data obtained via [Google Maps Javascript API](https://developers.google.com/maps/documentation/javascript/reference) plus weather data provided by the [OpenWeatherMap API](http://openweathermap.org/current). Regarding the project's structure, Knockout's support for components and custom elements has been leveraged in combination with [Browserify](http://browserify.org/) to break down and encapsulate the project's functionality and user interface into discrete components thereby simplifying development. Last, but not least, a build process using [Gulp](http://gulpjs.com/) has been put in place to enable support for [SASS](http://sass-lang.com/) and [ES2015](http://es6-features.org/).

Thanks to [Fabio Vergani](https://sites.google.com/site/gmapsdevelopment/) for his very illustrative real estate Google Map icon and to Sam Herbert for his sober yet elegant [color scheme for Google Maps](https://snazzymaps.com/style/44/mapbox).

---

## License

This project is licensed under the terms of the [**MIT**](https://opensource.org/licenses/MIT) license.
