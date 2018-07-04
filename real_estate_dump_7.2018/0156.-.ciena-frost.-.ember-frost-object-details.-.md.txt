[ci-img]: https://img.shields.io/travis/ciena-frost/ember-frost-object-details.svg "Travis CI Build Status"
[ci-url]: https://travis-ci.org/ciena-frost/ember-frost-object-details

[cov-img]: https://img.shields.io/coveralls/ciena-frost/ember-frost-object-details.svg "Coveralls Code Coverage"
[cov-url]: https://coveralls.io/github/ciena-frost/ember-frost-object-details

[npm-img]: https://img.shields.io/npm/v/ember-frost-object-details.svg "NPM Version"
[npm-url]: https://www.npmjs.com/package/ember-frost-object-details

[ember-observer-badge]: http://emberobserver.com/badges/ember-frost-object-details.svg "Ember Observer score"
[ember-observer-badge-url]: http://emberobserver.com/addons/ember-frost-object-details

[ember-img]: https://img.shields.io/badge/ember-2.3+-orange.svg "Ember 2.3+"

[![Travis][ci-img]][ci-url] [![Coveralls][cov-img]][cov-url] [![NPM][npm-img]][npm-url]

[bithound-img]: https://www.bithound.io/github/ciena-frost/ember-frost-object-details/badges/score.svg "bitHound"
[bithound-url]: https://www.bithound.io/github/ciena-frost/ember-frost-object-details

# ember-frost-object-details
###### Dependencies

![Ember][ember-img]
[![NPM][npm-img]][npm-url]

###### Health

[![Travis][ci-img]][ci-url]
[![Coveralls][cov-img]][cov-url]

###### Security

[![bitHound][bithound-img]][bithound-url]

###### Ember Observer score
[![EmberObserver][ember-observer-badge]][ember-observer-badge-url]

An object details page packages together all details about an object in a full page of real estate. The
ember-frost-object-details component will provide you free animations, styles and the frame of the page with
simple setup.

## Installation
```
ember install ember-frost-object-details
```

## API
Detailed API and example usage can be found in the sample application in `tests/dummy`, which is also running at http://ciena-frost.github.io/ember-frost-object-details

### Ember-elsewhere

This addon uses the [ember-elsewhere](https://github.com/ef4/ember-elsewhere) to manage the tabs, to put the tab in
the right location

### Testing with ember-hook
This addon has been optimized for use with [ember-hook](https://github.com/Ticketfly/ember-hook). You can set a `hook`
name on your object details template.
This will allow you to access the internal object details content for testing.

## Development
### Setup
```
git clone git@github.com:ciena-frost/ember-frost-object-details.git
cd ember-frost-object-details
npm install && bower install
```

### Development Server
A dummy application for development is available under `ember-frost-object-details/tests/dummy`.
To run the server run `ember server` (or `npm start`) from the root of the repository and
visit the app at http://localhost:4200.

### Testing
Run `npm test` from the root of the project to run linting checks as well as execute the test suite
and output code coverage.
