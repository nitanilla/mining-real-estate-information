### About

Estonian real estate listing parser.

### Usage

```
npm install
node scrape_kv.js | node addressify.js | node cadify.js
```

To visualize the results:

```
npm install -g csv2geojson geojsonio-cli 
node scrape_kv.js | node addressify.js | node cadify.js | csv2geojson | geojsonio
```