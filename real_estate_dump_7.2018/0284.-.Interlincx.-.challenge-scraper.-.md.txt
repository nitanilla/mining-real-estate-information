# Scrape Code Challenge

This challenge is create a module that scrapes real estate information [this page](https://losangeles.craigslist.org/search/apa). The module should return data like this:

```js
[
  {
    title: 'OCEAN FRONT CONDO FOR LEASE',
    url: 'https://losangeles.craigslist.org/wst/apa/d/ocean-front-condo-for-lease/6222223652.html',
    time: '2017-07-28 07:19',
    price: '$4000',
    bedrooms: '2br',
    size: '1320ft2',
    neighborhood: 'Redondo Beach'
  },
  ...
]
```

### Setup & Running

*  run ```npm i``` in order to install required packages.

* run `npm test` in order to get the tests output.

## Rules:

* Create a module `index.js` that exports a function.

* This function will asynchronously return the number of desired real estate listings. See `test.js` for details.

* Do not modify `test.js`.

* Follow these [coding style guidelines](https://gist.github.com/davidguttman/9fbdd0e9ee1fb3b33f5cf693195f2edb#code-style).

* Do not add any other npm modules.

* In order to complete the challenge, **all** tests should be passing like in example bellow:

```bash
> node test.js && standard

TAP version 13
# should get 50 listings
ok 1 should not error
ok 2 should be equal
# should get 120 listings
ok 3 should not error
ok 4 should be equal
# should get 250 listings
ok 5 should not error
ok 6 should be equal
# should get correct listings format
ok 7 should not error
ok 8 should match expected

1..8
# tests 8
# pass  8

# ok
```
