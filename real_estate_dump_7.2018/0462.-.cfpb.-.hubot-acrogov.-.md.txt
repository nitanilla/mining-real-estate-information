# hubot-acrogov [![Build Status][travis-image]][travis-url] [![NPM version][npm-image]][npm-url]

A hubot script that defines acronyms and other terms used by government agencies

See [`src/acrogov.coffee`](src/acrogov.coffee) for full documentation.

## Installation

In hubot project repo, run:

`npm install hubot-acrogov --save`

Then add **hubot-acrogov** to your `external-scripts.json`:

```json
["hubot-acrogov"]
```

## Commands

```
hubot define <term> - returns the definition of the term
hubot define <term> as <definition> - save the definition of a term
hubot stop defining <term> - removes a term and all of its definitions
hubot stop defining <term> as <definition> - removes the specified definition of the term
```

## Sample Interaction

```
user1>> hubot define TRID as TILA-RESPA Integrated Disclosure — and TILA-RESPA stands for Truth in Lending Act-Real Estate Settlement Procedures Act
hubot>> I added TRID.

user2>> hubot define TRID
hubot>> TRID stands for TILA-RESPA Integrated Disclosure — and TILA-RESPA stands for Truth in Lending Act-Real Estate Settlement Procedures Act
```

## Definitions
The starter definitions are for terms in use at the [Consumer Financial Protection Bureau](http://www.consumerfinance.gov). You can use your own set by overwriting src/json/acro.json.

If you want to use a private set of definitions, you can alternatively set an environment variable called `HUBOT_ACRO_PRIVATE_FILE` on your server that points to the location of your private json file. The hubot will load those definitions instead of the public ones.

[npm-image]: https://img.shields.io/npm/v/hubot-acrogov.svg?maxAge=2592000&style=flat-square
[npm-url]: https://www.npmjs.com/package/hubot-acrogov
[travis-image]: https://img.shields.io/travis/cfpb/hubot-acrogov.svg?maxAge=2592000&style=flat-square
[travis-url]: https://travis-ci.org/cfpb/hubot-acrogov
