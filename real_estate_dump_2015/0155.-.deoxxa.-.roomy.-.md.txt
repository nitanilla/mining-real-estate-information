[![build status](https://secure.travis-ci.org/deoxxa/roomy.png)](http://travis-ci.org/deoxxa/roomy)

Roomy
=====

Parse Japanese real estate room descriptions like 1LDK into objects.

Overview
--------

With roomy, you can parse strings like `1LDK` into objects like this:

```json
{
  "rooms": 1,
  "living_room": true,
  "dining_room": true,
  "kitchen": true
}
```

You can also turn them back into their string representation!

Installation
------------

> $ npm install roomy

OR

> $ git clone git://github.com/deoxxa/roomy.git node_modules/roomy

Usage
-----

```javascript
#!/usr/bin/env node

var roomy = require("roomy");

var object = roomy.parse("1LDK");

console.log(object);

var string = roomy.generate(object);

console.log(string);
```

License
-------

3-clause BSD. A copy is included with the source.

Contact
-------

* GitHub ([deoxxa](http://github.com/deoxxa))
* Twitter ([@deoxxa](http://twitter.com/deoxxa))
* ADN ([@deoxxa](https://alpha.app.net/deoxxa))
* Email ([deoxxa@fknsrs.biz](mailto:deoxxa@fknsrs.biz))
