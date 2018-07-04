# newyorktimes

A Node.js wrapper for New York Times' API.

```js
var nyt = require('newyorktimes')(keys);
```

## APIs

* [Article Search](#Article-Search)
* [Best Sellers](#Best-Sellers)
* [Campaign Finance](#Campaign-Finance)
* [Community](#Community)
* [Congress](#Congress)
* [Districts](#Districts)
* [Event Listings](#Event-Listings)
* [Geographic](#Geographic)
* [Most Popular](#Most-Popular)
* [Movie Reviews](#Movie-Reviews)
* [Real Estate](#Real-Estate)
* [Semantic](#Semantic)
* [Times Newswire](#Times-Newswire)
* [Timestags](#Timestags)

---

### <a name="Article-Search"></a>Article Search
Search Times articles from 1851 to today, retrieving headlines, abstracts and links to associated multimedia.

### <a name="Best-Sellers"></a>Best Sellers
Get data from all New York Times best-seller lists, including rank history for specific best sellers.

### <a name="Campaign-Finance"></a>Campaign Finance
Get presidential campaign contribution and expenditure data based on United States Federal Election Commission filings.

### <a name="Community"></a>Community
Get comments by NYTimes.com users.

### <a name="Congress"></a>Congress
Get U.S. Congressional vote data, including information about specific House and Senate members.

### <a name="Districts"></a>Districts
Get political districts based on a pair of coordinates. Currently, the Districts API is limited to New York City.

### <a name="Event-Listings"></a>Event Listings
Get information about hand-picked events in New York City and the surrounding area.

### <a name="Geographic"></a>Geographic
Use linked data to enhance location concepts used in The New York Times' controlled vocabulary.

### <a name="Most-Popular"></a>Most Popular
Get links and metadata for the blog posts and articles that are most frequently e-mailed, shared and viewed by NYTimes.com readers.

### <a name="Movie-Reviews"></a>Movie Reviews
Get links to reviews and NYT Critics' Picks, and search movie reviews by keyword.

### <a name="Real-Estate"></a>Real Estate
Get aggregate data for real estate listings and sales in New York City.

### <a name="Semantic"></a>Semantic
Get access to the people, places, organizations and descriptors that make up the controlled vocabulary used as metadata by The New York Times.

### <a name="Times-Newswire"></a>Times Newswire
Get links and metadata for Times articles in an up-to-the-minute stream.

### <a name="Timestags"></a>Timestags
Get standardized terms that match your search query, and filter by Times dictionaries.

## Quickstart

- Reqest an API key: http://developer.nytimes.com/apps/register
- View your keys at: http://developer.nytimes.com/apps/myapps
- Create a file `.env` and format environment file with keys as in `test.js`
- Follow the example

## Example

Call the [API](http://developer.nytimes.com/docs) url directly without needing to add the API key.

```js
var keys = {
  article_search: 'API_KEY',
  best_sellers: 'API_KEY',
  campaign_finance: 'API_KEY',
  community: 'API_KEY',
  congress: 'API_KEY',
  districts: 'API_KEY',
  event_listings: 'API_KEY',
  geo: 'API_KEY',
  most_popular: 'API_KEY',
  movie_reviews: 'API_KEY',
  real_estate: 'API_KEY',
  semantic: 'API_KEY',
  times_newswire: 'API_KEY',
  timestags: 'API_KEY'
};
var nyt = require('newyorktimes')(keys);
nyt.query('http://api.nytimes.com/svc/semantic/v2/geocodes/query.json?country_code=US', function (err, json) {
  console.log(json);
});
```

Note: HTTPS works as well.

## Tests

Run tests with

```sh
npm test
```
