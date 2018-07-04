#denmark-real-estate-valuation [![Build Status](https://travis-ci.org/denmark-io/denmark-real-estate-valuation.svg?branch=master)](https://travis-ci.org/denmark-io/denmark-real-estate-valuation)

> A stream of real estate valuations given a zipcode and streetname

## Installation

```sheel
npm install denmark-real-estate-valuation
```

## Documentation

```javascript
RealEstateValuation = require('denmark-real-estate-valuation')
```

This is a class constructor with the signature `RealEstateValuation(query)`,
it returns a readable stream.

query is an object that could specify the area (either `zipCode` or `municipalityCode`)
and the street name (`streetName`). If the `municipalityCode` is used
a street code (`streetCode`) can be used instead of street name.

```javascript
const valuations = RealEstateValuation({
  zipCode: 2800,
  streetName: 'Lyngby Hovedgade'
});

// alternatively: { municipalityCode: 173, streetName: 'Lyngby Hovedgade' }
// alternatively: { municipalityCode: 173, streetCode: 535 }

valuations.on('data', function (property) {
  property = {
    id: 51002,
    houseNumber: '1A',
    floor: '2',
    type: 'Ejerlejl. iøvrigt',
    landValue: 10210000, // danish kroner (DKK)
    houseValue: 30500000 // danish kroner (DKK)
  };

  // The real estate value is `property.landValue + property.houseValue`.
});
```

## Source

The source is: http://www.vurdering.skat.dk/borger/ejendomsvurdering/Soeg2.do
The webpage does not provide an API, so this module scrapes the data from it.
