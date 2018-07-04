# rets.js [![Travis](https://img.shields.io/travis/retsr/rets.js.svg)](https://travis-ci.org/retsr/rets.js) [![Coverage Status](https://coveralls.io/repos/retsr/rets.js/badge.svg?branch=master)](https://coveralls.io/r/retsr/rets.js?branch=master)

> Simplified RETS Node Client

rets.js aims to simplify interacting with Real Estate Transaction Standard
compliant servers using Node.js. Specifically RETS Version 1.8.
It is an effort to bring a properly functioning and performant libRETS
implementation to the Node.js community.

This library is _not_ a libRETS wrapper, but seeks to provide a
similar API interface while offering additional feature support that Node.js
developers have come to rely on like events and streaming.

A secondary but still important goal is to keep the code as simple to read as
possible to help developers understand the RETS Specification.

More information about RESO and the RETS 1.8 Specification can be found at the
[RESO](http://www.reso.org) and [Specification Documentation](http://www.reso.org/specifications)
sites respectively.

## Install

    npm install --save rets.js

## Testing

    npm run test-watch

## Examples

You can find a number of examples in the [examples](examples) directory

## Contributing

See [CONTRIBUTING](CONTRIBUTING.md) for details on submitting patches and the contribution workflow.

## License

See [LICENSE](LICENSE)
