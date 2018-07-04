# MUSA-620-Week-6: Web Scraping Part 1



### Links:
* [HTML vs DOM, Example 1](https://blueshift.io/selectors2.html)
* [HTML vs DOM, Example 2](https://blueshift.io/selectors2.html)
* [rvest package](https://cran.r-project.org/web/packages/rvest/rvest.pdf) for parsing HTML

## Getting to Know Your Browser's Web Inspector

### Elements tab

Use the elements tab to explore a webpage's DOM.

##### Examples:
* [Simple example](https://blueshift.io/selectors2.html)
* Grab text from sites that have copying disabled: [NY Times](https://www.nytimes.com/2016/08/23/upshot/50-years-of-electoral-college-maps-how-the-us-turned-red-and-blue.html)
* Find and download a hidden video file: [Imgur](https://i.imgur.com/9M4Rsf0.gifv)

### Network tab

Use the network tab to find the data used in these webpages.

##### [FiveThirtyEight: Congressional Districts](https://projects.fivethirtyeight.com/redistricting-maps/)
* [Congressional district map](https://projects.fivethirtyeight.com/redistricting-maps/US-current.topo.json)

##### [WSJ: California Drought](http://graphics.wsj.com/californias-long-challenge-with-drought/)
* [CA outline](http://graphics.wsj.com/californias-long-challenge-with-drought/data/shared/california.topo.json)
* [Drought isocrones](http://graphics.wsj.com/californias-long-challenge-with-drought/data/drought/drought.ca.topo.json)
* [Major cities](http://graphics.wsj.com/californias-long-challenge-with-drought/data/shared/major_cities.topo.json)
* [Population affected](http://graphics.wsj.com/californias-long-challenge-with-drought/data/drought/population-affected.csv)

![California drought map](https://github.com/MUSA-620-Spring-2018/MUSA-620-Week-6/blob/master/california-drought-map.png)

*Data: [Wall Street Journal](http://graphics.wsj.com/californias-long-challenge-with-drought/) / code: [web-inspector-data.r](https://github.com/MUSA-620-Spring-2018/MUSA-620-Week-6/blob/master/web-inspector-data.R)*

##### [Washington Post: US Sunlight Map](https://www.washingtonpost.com/news/wonk/wp/2015/07/13/map-where-americas-sunniest-and-least-sunny-places-are/)
* See if you can you can find the data to recreate their sunlight map yourself. *The steps for doing this have now been added to [web-inspector-data.r](https://github.com/MUSA-620-Spring-2018/MUSA-620-Week-6/blob/master/web-inspector-data.R)*

![Map of average daily sunlight by county](https://github.com/MUSA-620-Spring-2018/MUSA-620-Week-6/blob/master/daily-sunlight-by-county-2.png)

*Data: [Washington Post](https://www.washingtonpost.com/news/wonk/wp/2015/07/13/map-where-americas-sunniest-and-least-sunny-places-are/) / code: [web-inspector-data.r](https://github.com/MUSA-620-Spring-2018/MUSA-620-Week-6/blob/master/web-inspector-data.R)*

##### [The Economist: Property Values by US County](https://www.economist.com/blogs/graphicdetail/2015/04/daily-chart-2)
* Sometimes data will be hidden in .js files: [county-level real estate values](https://infographics.economist.com/2015/ASBTest/Land/js/countyData.js?__sbCache=0.26521743179319657)
* Used as the data source for the map below

[Total residential property value of each US county](http://metrocosm.com/the-housing-value-of-every-county-in-the-u-s/)

![map of property values USA](http://i0.wp.com/metrocosm.com/wp-content/uploads/2015/10/cartogram-property-values.gif)


