# toronto housing
[MongoHouse](http://mongohouse.com/) & [OhMyHome](http://watch.ohmyhome.ca) are real estate websites targeted at providing information on the Toronto/GTA housing market. One of the unique features of the site is that it includes sale prices, which is generally information that is only available to realtors.

Monitoring different areas of the Toronto housing market could be useful for understanding which areas have seen the highest price increases and could be prone to a correction. Alternatively, if and when a general housing market correction occurs, it would be useful to see which areas are hit the hardest.


## Getting the data
### MongoHouse

MongoHouse allows user to choose to view new listings or sold records, and displays the data in a map view.

<p align="center">
<img src="./img/mongo_map.png" width="1500px" >
</p>

On Chrome, you can open up developer tools to view the web requests going on behind the scenes. As you can see in the picture below, a call is made to the MongoHouse API with the different property IDs passed in as parameters.

<p align="center">
<img src="./img/mongo_request.png" width="1500px" >
</p>

And the response is a beautifully formatted JSON object:

<p align="center">
<img src="./img/mongo_response.png" width="500px" >
</p>

Lucky for us, MongoHouse uses client-side API calls to retrieve the data shown across the site. Using the Python requests module we can easily make the same API calls programatically.

#### Authentication

Most of the MongoHouse APIs require no authentication in order to retrieve the data. However, in order to view the sale prices an account is required.

For this project, authentication was accomplished using the `Login.py` module.

First, a session is initialized by hitting the MongoHouse homepage. This web request returns a session ID in the response cookies.

```python
init_headers = {
  'User-Agent': ua[self.user['browser']], ## randomly generated user agent string.
  "Host": "www.mongohouse.com",
  "Proxy-Connection": "keep-alive",
  "Upgrade-Insecure-Requests": 1,
  "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8",
  "Accept-Encoding": "gzip, deflate, sdch",
  "Accept-Language": "en-US,en;q=0.8,fr;q=0.6"
}

session = requests.session()
r = session.get('http://www.mongohouse.com/',headers=init_headers)

cookies = session.cookies.get_dict()
session_id = cookies['sessionId']
```

Using this session ID, a POST request can be sent to the sign in API along with the account's username and password.

```python
r_payload = {'username': self.user['UID'], 'password': self.user['PWD']}
resp = session.post('http://www.mongohouse.com/api/auth/signin',r_payload,
                    headers=self.headers)
if resp.status_code == 200:
    print ('Session successfully established')
else:
    print ('Unable to create session. Session response %s' % resp)
```

Once the login is accomplished, simple requests can be made to retrieve the data from each API:

```python
r = session.get(url)
data = json.loads(r.text) ## or r.json() can be used
```



### OhyMyHome
OhMyHome requires no login/authentication, making the data retrieval much easier. Their API can be accessed by sending a post request to `http://watch.ohmyhome.ca/HouseForSale/HouseForSale.php` with a request payload like `{"latitude1":43.044628815323996,"longitude1":-80.78431278320312,"latitude2":43.84227688250318,"longitude2":-77.94709354492187}`.

Originally, I very naively thought I could get all the data by pinging the API with lat/lon coordinates that encompassed all of Ontario. This resulted in a server error being thrown and no data returned.

To fix this, I specify a big area I want to retrieve results for, and the number of divisions to create within that area.

```python
## coordinates
SOUTH = 42.7347443837978
WEST = -82.05335556083372
NORTH = 45.317234079179435
EAST = -77.49128280692747

DIVISIONS = 15
```

Note that 15 "divisions" means 15 slices vertically and 15 slices horizontally. The `_buildPayloads` function is called to split the specified area into 225 sub-areas (i.e. `15*15`), and return the coordinates for each of those areas. I arrived at 15 divisions through trial and error, where I increased the number of divisions until I wasn't getting server errors.

```python
def _buildPayloads(self):
  lat_coords, long_coords = self._getCoords()
  payloads = []
  for x in range(1, config.DIVISIONS+1):
      for y in range(1, config.DIVISIONS+1):
          payloads.append({
              "latitude1": lat_coords[y-1],
              "longitude1": long_coords[x-1],
              "latitude2": lat_coords[y],
              "longitude2": long_coords[x]
              })

  return payloads

def _getCoords(self):
  south = config.SOUTH
  west = config.WEST
  lat_div = (config.NORTH - config.SOUTH)/config.DIVISIONS
  long_div = (abs(config.WEST) - abs(config.EAST))/config.DIVISIONS
  lat_coords = [south]
  long_coords = [west]

  for x in range(0, config.DIVISIONS):
      south += lat_div
      west += long_div
      lat_coords.append(south)
      long_coords.append(west)
  return lat_coords, long_coords
```
The API is then called for each sub-area, as demonstrated below:

<p align="center">
<img src="./img/grid.gif" width="1500px" >
</p>

## Data ETL Process
To clean and transform the data from the JSON response to the format required by the Postgres database, I created a `FIELD_MAP` parameter in `config.py` which defines the field name in the JSON response and which functiion should be used to validate/transform the field.

Each field in `FIELD_MAP` maps to a destination column in the Postgres database (see [schema.sql](https://github.kdc.capitalone.com/IanWhitestone/mongo-house/blob/master/queries/schema.sql)). Right now the mapping is order based (i.e. the first field `_id` maps to the first column in the `sale_records` table and so on).

```python

FIELD_MAP = {
    'sale': [
        {'name': '_id', 'func': 'check_varchar', 'length': 50},
        {'name': 'Address1', 'func': 'check_varchar', 'length': 200},
        {'name': 'Address2', 'func': 'check_varchar', 'length': 200},
        {'name': 'Bedrooms', 'func': 'check_varchar', 'length': 5},
        {'name': 'Community', 'func': 'check_varchar', 'length': 100},
        {'name': 'PostalCode', 'func': 'check_varchar', 'length': 10},
        {'name': 'Bedrooms', 'func': 'check_varchar', 'length': 10},
        {'name': '_Sold', 'func': 'check_int'},
        {'name': '_List', 'func': 'check_int'},
        {'name': '_Sold_Date', 'func': 'check_date'},
        {'name': '_Contract_Date', 'func': 'check_date'},
        {'name': 'Undefined', 'func': 'get_property_type'}

    ], ...
```

The functions referenced in the `FIELD_MAP` are housed in the `DataCleaning.py` module. Using the `getattr()` Python function, the functions can be called from their string names.

```python
fields = []
for field in config.FIELD_MAP[record_type]:
  val = data.get(field['name'], None)
  if val:
      cleaned_val = getattr(DataCleaning, field['func'])(val=val,
                      length=field.get('length',0))
  else:
      cleaned_val = None
  fields.append(cleaned_val)
```
