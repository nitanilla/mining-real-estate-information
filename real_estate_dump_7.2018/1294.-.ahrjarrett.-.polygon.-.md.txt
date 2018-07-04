# Real Estate Polygon App

Demo: [Polygon Demo](https://polygonpolygon.herokuapp.com/)

### Instructions:
Click at least twice on the map to create a line, three times or more to create a polygon. On the right are operations you can perform, including a log of the coordinates of the line/polygon and a function that will check a JSON array full of coordinates and return which, if any, are contained inside the polygon and fall within the designated price range (click 'See JSON Data' to see all coordinates).

Note that the Polygon is draggable and editable; as of now, 'Log Path' and 'Check Against Map' will need to be run again in order to re-compute coordinates. Also note that there is an arbitrary limit on the number of pin-drops the polygon will accept (6).

To start hacking locally:

```
$ git clone https://github.com/ahrjarrett/polygon
$ cd polygon
$ npm i -g watchify nodemon
$ npm run dev
# in a separate terminal window:
$ npm run watch
```

**Notes:**
- 10/30/17: ajax calls stopped working (not the mongo queries, as i thought at first), so as a temporary fix i swapped jquery out for axios and attached the promise resolution to window.homes. currently not working for polygon, requiring a more substantial fix/code review.

### Todo:
- saveHome and savePoly are broken, fix so they persist data to DB again
- ~~Load home data from database instead of data.json~~
- ~~Turn each coordinate and address into dynamic link to its raw data~~
- ~~Add price filter~~
- ~~Bug: Log Addresses & Log Coordinates append, without removing children~~
- ~~repopulate #show-poly with saved polygons for reference later~~
- ~~Hone Polygram and Home schema, add error handling~~
- ~~figure out how eventListeners work when layered on Polygons (no rightclick event?)~~
- ~~Save Polygrams in db for reference later~~
- ~~fix ajax sync problem (open console for e.message)~~
- Remove cruft in public/javascripts (unused files, required fns that aren't invoked, etc.)
- asynchronous req from geocode returns an array that's out of order, causes exceptions
- POST request: /save-home *make it work at all*
- POST request: /save-poly *make it work again*
- figure out how to trim, or otherwise force JSON input to work (or just rethink the whole thing)
- *OR*: get vertices dynamically, or from a DB query
- Bug: Clear log doesn't empty results array, which means it keeps accumulating state
- Refactor filtering logic for easier reuse later
- add one more form to right interface (toggle showPolygon(s))?
