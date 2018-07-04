# Project 1 - Simple Buyer Guide

#### Group Name: PyitUp
-------------------------------
#### Member Name: 
#### Lindsay Yan: https://www.linkedin.com/in/lindsay-yan-8a09469b/
#### Nana Zhuohui Liang: https://www.linkedin.com/in/nana-zhuohui-liang-22a9302a/
#### Sonia Yang: https://www.linkedin.com/in/sonia-yang-69504438/
#### Sue Del Carpio Bellido: https://www.linkedin.com/in/suedelcarpiobellido/
#### Yinling Wang: 

### Purpose 

* Building a simple home guide to home buyers on multiple factors associated with house prices in order to make the buyers more informed when they are making buying decisions

### Scope: 

* Target Buyer profile: first time buyer, school focus buyer (for kids), professional buyer, rich buyer, investment buyer
* Region: LA County
* Time: Most Recent data (Data range from 2016, 2017 mainly)

* Database: 
a. Census data: https://github.com/CommerceDataService/census-wrapper
⋅⋅⋅The most updated census data from wrapper is 2016
b. Crime data: https://catalog.data.gov/dataset/crime-data-from-2010-to-present (from: data.lacity.org)
⋅⋅⋅Crime Data was not incorporated into the final project due to the size of data and the limiation of pulling Geo info from google. 
c. School Ranking Data: http://school-ratings.com/counties/Los_Angeles.html
⋅⋅⋅School Ranking Data is provided directly from the website not API pulling needed	
d. Zillow API: https://www.zillow.com/webservice/GetSearchResults.htm?
e. Google Data: various API link for different purpose: Geocode, search amenities, etc.

### Metrics:
1. Average House price by city
2. Average School ranking by city
3. Employment data by city
4. number of Shops by city
5. Public Transporation by city
6. Location data
7. Other Housing Data

### Recommendation: End Produce - What we need to provide to the Client:
* Various Graph to compare different attribute by city (more than just housing price) 
* Suggest City choice to different Buyers 


### Code 
#### 1-1.LA_cities_Lat_lng_code
```python
# Dependencies
import requests
import json
import pandas as pd

# Google developer API key
from config import gkey1

# Target city #### Getting coordinates from Geogle GeoCoding API ###API 1
city_address=pd.read_csv('../Raw_Data/1-1.city_codes.csv',sep=',')
```


```python
LA_cities=city_address[city_address['Metro']=='Los Angeles']
```


```python
list_city=['Los Angeles',
'Long Beach',
'Santa Clarita',
'Glendale',
'Palmdale',
'Lancaster',
'Pomona',
'Torrance',
'Pasadena',
'Inglewood',
'El Monte',
'Downey',
'West Covina',
'Norwalk',
'Burbank',
'Compton',
'South Gate',
'Whittier',
'Hawthrone',
'Alhambra']
```


```python
LA_cities.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Region</th>
      <th>State</th>
      <th>Metro</th>
      <th>County</th>
      <th>Code</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Los Angeles</td>
      <td>CA</td>
      <td>Los Angeles</td>
      <td>Los Angeles</td>
      <td>2</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Long Beach</td>
      <td>CA</td>
      <td>Los Angeles</td>
      <td>Los Angeles</td>
      <td>28</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Anaheim</td>
      <td>CA</td>
      <td>Los Angeles</td>
      <td>Orange</td>
      <td>42</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Santa Ana</td>
      <td>CA</td>
      <td>Los Angeles</td>
      <td>Orange</td>
      <td>44</td>
    </tr>
    <tr>
      <th>97</th>
      <td>Irvine</td>
      <td>CA</td>
      <td>Los Angeles</td>
      <td>Orange</td>
      <td>98</td>
    </tr>
  </tbody>
</table>
</div>




```python
final=[]
for i in range(len(LA_cities)):
    target=LA_cities.iloc[i,:]
    table_final={}
    table_final['Region']=target['Region']
    table_final['State']=target['State']
    if table_final['Region'] in list_city:
        final.append(table_final)
final = pd.DataFrame(final)
final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Region</th>
      <th>State</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Lancaster</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Santa Clarita</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Pomona</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Torrance</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Pasadena</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Inglewood</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Compton</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Downey</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>12</th>
      <td>West Covina</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Norwalk</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burbank</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>15</th>
      <td>South Gate</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>16</th>
      <td>El Monte</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Whittier</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alhambra</td>
      <td>CA</td>
    </tr>
  </tbody>
</table>
</div>




```python
#regions=pd.DataFrame(final)
list_Region=final['Region']
list_Region
```




    0       Los Angeles
    1        Long Beach
    2          Glendale
    3         Lancaster
    4          Palmdale
    5     Santa Clarita
    6            Pomona
    7          Torrance
    8          Pasadena
    9         Inglewood
    10          Compton
    11           Downey
    12      West Covina
    13          Norwalk
    14          Burbank
    15       South Gate
    16         El Monte
    17         Whittier
    18         Alhambra
    Name: Region, dtype: object




```python
# Run a request to endpoint and convert result to json
target=[]
for i in range(len(list_Region)):
    
    target_city=list_Region[i]
    target_url = "https://maps.googleapis.com/maps/api/geocode/json?" \
     "address=%s&key=%s" % (target_city, gkey1)
    geo_data = requests.get(target_url).json()
    #print(geo_data)
    R1=geo_data["results"][0]
    #print(R1)
    for a in range(len(R1)):
        R2=R1["geometry"]
        print(R2['location']['lat'])
        for j in R2:
            citi={}
            citi['lat']=R2["location"]["lat"]
            citi['lng']=R2["location"]["lng"]
            citi['northeast_Lat']=R2["bounds"]["northeast"]["lat"]
            citi['northeast_Lng']=R2["bounds"]["northeast"]["lng"]
            citi['southwest_Lat']=R2["bounds"]["southwest"]["lat"]
            citi['southwest_Lng']=R2["bounds"]["southwest"]["lng"]
            citi['address']=target_city
    target.append(citi)
```

    34.0522342
    34.0522342
    34.0522342
    34.0522342
    34.0522342
    33.7700504
    33.7700504
    33.7700504
    33.7700504
    33.7700504
    34.1425078
    34.1425078
    34.1425078
    34.1425078
    34.1425078
    40.0378755
    40.0378755
    40.0378755
    40.0378755
    40.0378755
    34.5794343
    34.5794343
    34.5794343
    34.5794343
    34.5794343
    34.3916641
    34.3916641
    34.3916641
    34.3916641
    34.3916641
    34.055103
    34.055103
    34.055103
    34.055103
    34.055103
    33.8358492
    33.8358492
    33.8358492
    33.8358492
    33.8358492
    34.1477849
    34.1477849
    34.1477849
    34.1477849
    34.1477849
    33.9616801
    33.9616801
    33.9616801
    33.9616801
    33.9616801
    33.8958492
    33.8958492
    33.8958492
    33.8958492
    33.8958492
    33.9401088
    33.9401088
    33.9401088
    33.9401088
    33.9401088
    34.0686208
    34.0686208
    34.0686208
    34.0686208
    34.0686208
    41.11774399999999
    41.11774399999999
    41.11774399999999
    41.11774399999999
    41.11774399999999
    34.1808392
    34.1808392
    34.1808392
    34.1808392
    34.1808392
    33.954737
    33.954737
    33.954737
    33.954737
    33.954737
    34.0686206
    34.0686206
    34.0686206
    34.0686206
    34.0686206
    33.9791793
    33.9791793
    33.9791793
    33.9791793
    33.9791793
    34.095287
    34.095287
    34.095287
    34.095287
    34.095287
    


```python
address_coordinate=pd.DataFrame(target)
address_coordinate
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>address</th>
      <th>lat</th>
      <th>lng</th>
      <th>northeast_Lat</th>
      <th>northeast_Lng</th>
      <th>southwest_Lat</th>
      <th>southwest_Lng</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>34.052234</td>
      <td>-118.243685</td>
      <td>34.337306</td>
      <td>-118.155289</td>
      <td>33.703652</td>
      <td>-118.668176</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>33.770050</td>
      <td>-118.193740</td>
      <td>33.885459</td>
      <td>-118.063253</td>
      <td>33.714957</td>
      <td>-118.248966</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>34.142508</td>
      <td>-118.255075</td>
      <td>34.267232</td>
      <td>-118.182005</td>
      <td>34.118761</td>
      <td>-118.307849</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Lancaster</td>
      <td>40.037875</td>
      <td>-76.305514</td>
      <td>40.073041</td>
      <td>-76.254084</td>
      <td>40.006910</td>
      <td>-76.346614</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>34.579434</td>
      <td>-118.116461</td>
      <td>34.661043</td>
      <td>-117.915747</td>
      <td>34.509813</td>
      <td>-118.287107</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Santa Clarita</td>
      <td>34.391664</td>
      <td>-118.542586</td>
      <td>34.477524</td>
      <td>-118.376071</td>
      <td>34.340498</td>
      <td>-118.613192</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Pomona</td>
      <td>34.055103</td>
      <td>-117.749991</td>
      <td>34.112936</td>
      <td>-117.711067</td>
      <td>34.018512</td>
      <td>-117.828817</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Torrance</td>
      <td>33.835849</td>
      <td>-118.340629</td>
      <td>33.887061</td>
      <td>-118.308127</td>
      <td>33.780217</td>
      <td>-118.394091</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Pasadena</td>
      <td>34.147785</td>
      <td>-118.144515</td>
      <td>34.251905</td>
      <td>-118.065479</td>
      <td>34.117037</td>
      <td>-118.198139</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Inglewood</td>
      <td>33.961680</td>
      <td>-118.353131</td>
      <td>33.982970</td>
      <td>-118.313391</td>
      <td>33.925177</td>
      <td>-118.378850</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Compton</td>
      <td>33.895849</td>
      <td>-118.220071</td>
      <td>33.923418</td>
      <td>-118.179962</td>
      <td>33.863086</td>
      <td>-118.263659</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Downey</td>
      <td>33.940109</td>
      <td>-118.133159</td>
      <td>33.972899</td>
      <td>-118.090262</td>
      <td>33.902455</td>
      <td>-118.170584</td>
    </tr>
    <tr>
      <th>12</th>
      <td>West Covina</td>
      <td>34.068621</td>
      <td>-117.938953</td>
      <td>34.092493</td>
      <td>-117.858261</td>
      <td>34.001855</td>
      <td>-117.967138</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Norwalk</td>
      <td>41.117744</td>
      <td>-73.408158</td>
      <td>41.171596</td>
      <td>-73.380562</td>
      <td>41.020449</td>
      <td>-73.474565</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burbank</td>
      <td>34.180839</td>
      <td>-118.308966</td>
      <td>34.221654</td>
      <td>-118.280109</td>
      <td>34.142367</td>
      <td>-118.370313</td>
    </tr>
    <tr>
      <th>15</th>
      <td>South Gate</td>
      <td>33.954737</td>
      <td>-118.212016</td>
      <td>33.966353</td>
      <td>-118.156119</td>
      <td>33.909964</td>
      <td>-118.231505</td>
    </tr>
    <tr>
      <th>16</th>
      <td>El Monte</td>
      <td>34.068621</td>
      <td>-118.027567</td>
      <td>34.100946</td>
      <td>-117.997465</td>
      <td>34.041393</td>
      <td>-118.072927</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Whittier</td>
      <td>33.979179</td>
      <td>-118.032844</td>
      <td>34.030716</td>
      <td>-117.965576</td>
      <td>33.928167</td>
      <td>-118.072246</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alhambra</td>
      <td>34.095287</td>
      <td>-118.127015</td>
      <td>34.111146</td>
      <td>-118.108181</td>
      <td>34.059921</td>
      <td>-118.164835</td>
    </tr>
  </tbody>
</table>
</div>




```python
#address_coordinate
address_coordinate.to_csv('../Raw_Data/1-1.LA_cities_Lat_lng_codes_data.csv',sep=',', index=None)
```

#### 1-2.City_Zipcode
```python
# Dependencies
import requests
import json
import pandas as pd

# Google developer API key (this key is obtained from https://www.zipcodeapi.com/API,
#the API code is temporate, need to grab a new one)
from config import zipkey

LA_counties=pd.read_csv('../Raw_Data/1-1.LA_cities_Lat_lng_codes_data.csv',sep=',')
```


```python
LA_counties.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>address</th>
      <th>lat</th>
      <th>lng</th>
      <th>northeast_Lat</th>
      <th>northeast_Lng</th>
      <th>southwest_Lat</th>
      <th>southwest_Lng</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>34.052234</td>
      <td>-118.243685</td>
      <td>34.337306</td>
      <td>-118.155289</td>
      <td>33.703652</td>
      <td>-118.668176</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>33.770050</td>
      <td>-118.193740</td>
      <td>33.885459</td>
      <td>-118.063253</td>
      <td>33.714957</td>
      <td>-118.248966</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>34.142508</td>
      <td>-118.255075</td>
      <td>34.267232</td>
      <td>-118.182005</td>
      <td>34.118761</td>
      <td>-118.307849</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Lancaster</td>
      <td>40.037875</td>
      <td>-76.305514</td>
      <td>40.073041</td>
      <td>-76.254084</td>
      <td>40.006910</td>
      <td>-76.346614</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>34.579434</td>
      <td>-118.116461</td>
      <td>34.661043</td>
      <td>-117.915747</td>
      <td>34.509813</td>
      <td>-118.287107</td>
    </tr>
  </tbody>
</table>
</div>




```python
list_address=LA_counties[['address']]

County=list_address['address']
State='CA'
```


```python
County
```




    0       Los Angeles
    1        Long Beach
    2          Glendale
    3         Lancaster
    4          Palmdale
    5     Santa Clarita
    6            Pomona
    7          Torrance
    8          Pasadena
    9         Inglewood
    10          Compton
    11           Downey
    12      West Covina
    13          Norwalk
    14          Burbank
    15       South Gate
    16         El Monte
    17         Whittier
    18         Alhambra
    Name: address, dtype: object




```python
###Get the list of Counties to get zipcode
list2=[]
for i in range(len(County)):
    
    target=County[i]
    t_state=State
    target_url="https://www.zipcodeapi.com/rest/"+zipkey+"/city-zips.json/"+target+"/"+t_state
    list2.append(target_url)
```


```python
list2[0]
```




    'https://www.zipcodeapi.com/rest/aBJPqUfiNCxoGUMdpUGdedHbovIzp8hrZsTOollpAvlaWnaq3nizIC91KMmThisq/city-zips.json/Los Angeles/CA'




```python
# Run a request to endpoint and convert result to json
target=[]

for i in range(len(County)):
   
    target_city=County[i]          
    target_url = list2[i]
    geo_data = requests.get(target_url).json()
    print (geo_data)
    R1=geo_data["zip_codes"]
    for j in range(len(R1)):
        dic={}
        dic['County']=target_city
        dic['zip']=R1[j] 
        target.append(dic)
```

    {'zip_codes': ['90001', '90002', '90003', '90004', '90005', '90006', '90007', '90008', '90009', '90010', '90011', '90012', '90013', '90014', '90015', '90016', '90017', '90018', '90019', '90020', '90021', '90022', '90023', '90024', '90025', '90026', '90027', '90028', '90029', '90030', '90031', '90032', '90033', '90034', '90035', '90036', '90037', '90038', '90039', '90040', '90041', '90042', '90043', '90044', '90045', '90046', '90047', '90048', '90049', '90050', '90051', '90052', '90053', '90054', '90055', '90056', '90057', '90058', '90059', '90060', '90061', '90062', '90063', '90064', '90065', '90066', '90067', '90068', '90070', '90071', '90072', '90073', '90074', '90075', '90076', '90077', '90078', '90079', '90080', '90081', '90082', '90083', '90084', '90086', '90087', '90088', '90089', '90091', '90093', '90095', '90096', '90099', '90101', '90102', '90103', '90189', '90069', '90090', '90094', '90230', '91331', '91335']}
    {'zip_codes': ['90801', '90802', '90803', '90804', '90805', '90806', '90807', '90808', '90809', '90810', '90813', '90814', '90815', '90822', '90831', '90832', '90833', '90834', '90835', '90840', '90842', '90844', '90845', '90846', '90847', '90848', '90853', '90888', '90899', '90745', '90746', '90747', '90749', '90755', '90895']}
    {'zip_codes': ['91201', '91202', '91203', '91204', '91205', '91206', '91207', '91208', '91209', '91210', '91221', '91222', '91225', '91226', '91214', '91224']}
    {'zip_codes': ['93534', '93535', '93536', '93539', '93584', '93586', '93551']}
    {'zip_codes': ['93550', '93551', '93552', '93590', '93591', '93599']}
    {'zip_codes': ['91350', '91380', '91382', '91383', '91390', '91310', '91321', '91322', '91351', '91354', '91355', '91381', '91384', '91385', '91386', '91387']}
    {'zip_codes': ['91766', '91767', '91768', '91769', '91797', '91799', '91765']}
    {'zip_codes': ['90501', '90502', '90503', '90504', '90505', '90506', '90507', '90508', '90509', '90510']}
    {'zip_codes': ['91101', '91102', '91103', '91104', '91105', '91106', '91107', '91109', '91110', '91114', '91115', '91116', '91117', '91121', '91123', '91124', '91125', '91126', '91129', '91131', '91182', '91184', '91185', '91188', '91189', '91191', '91199', '91108', '91118']}
    {'zip_codes': ['90301', '90302', '90303', '90304', '90305', '90306', '90307', '90308', '90309', '90310', '90311', '90312', '90313', '90397', '90398']}
    {'zip_codes': ['90220', '90221', '90222', '90223', '90224']}
    {'zip_codes': ['90239', '90240', '90241', '90242']}
    {'zip_codes': ['91790', '91791', '91792', '91793']}
    {'zip_codes': ['90650', '90651', '90652', '90659']}
    {'zip_codes': ['91501', '91502', '91503', '91504', '91505', '91506', '91507', '91508', '91510', '91521', '91522', '91523', '91526']}
    {'zip_codes': ['90280']}
    {'zip_codes': ['91731', '91732', '91734', '91735', '91733']}
    {'zip_codes': ['90601', '90602', '90603', '90604', '90605', '90606', '90607', '90608', '90609', '90610', '90612']}
    {'zip_codes': ['91801', '91802', '91803', '91804', '91841', '91896', '91899']}
    


```python
Table=pd.DataFrame(target)
Table.to_csv('1-2.zipcodes_in_LA_counties.csv',index=None)
```


```python
Table
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>County</th>
      <th>zip</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>90001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Los Angeles</td>
      <td>90002</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Los Angeles</td>
      <td>90003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Los Angeles</td>
      <td>90004</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Los Angeles</td>
      <td>90005</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Los Angeles</td>
      <td>90006</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Los Angeles</td>
      <td>90007</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Los Angeles</td>
      <td>90008</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Los Angeles</td>
      <td>90009</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Los Angeles</td>
      <td>90010</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Los Angeles</td>
      <td>90011</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Los Angeles</td>
      <td>90012</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Los Angeles</td>
      <td>90013</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Los Angeles</td>
      <td>90014</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Los Angeles</td>
      <td>90015</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Los Angeles</td>
      <td>90016</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Los Angeles</td>
      <td>90017</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Los Angeles</td>
      <td>90018</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Los Angeles</td>
      <td>90019</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Los Angeles</td>
      <td>90020</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Los Angeles</td>
      <td>90021</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Los Angeles</td>
      <td>90022</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Los Angeles</td>
      <td>90023</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Los Angeles</td>
      <td>90024</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Los Angeles</td>
      <td>90025</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Los Angeles</td>
      <td>90026</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Los Angeles</td>
      <td>90027</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Los Angeles</td>
      <td>90028</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Los Angeles</td>
      <td>90029</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Los Angeles</td>
      <td>90030</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>267</th>
      <td>Burbank</td>
      <td>91508</td>
    </tr>
    <tr>
      <th>268</th>
      <td>Burbank</td>
      <td>91510</td>
    </tr>
    <tr>
      <th>269</th>
      <td>Burbank</td>
      <td>91521</td>
    </tr>
    <tr>
      <th>270</th>
      <td>Burbank</td>
      <td>91522</td>
    </tr>
    <tr>
      <th>271</th>
      <td>Burbank</td>
      <td>91523</td>
    </tr>
    <tr>
      <th>272</th>
      <td>Burbank</td>
      <td>91526</td>
    </tr>
    <tr>
      <th>273</th>
      <td>South Gate</td>
      <td>90280</td>
    </tr>
    <tr>
      <th>274</th>
      <td>El Monte</td>
      <td>91731</td>
    </tr>
    <tr>
      <th>275</th>
      <td>El Monte</td>
      <td>91732</td>
    </tr>
    <tr>
      <th>276</th>
      <td>El Monte</td>
      <td>91734</td>
    </tr>
    <tr>
      <th>277</th>
      <td>El Monte</td>
      <td>91735</td>
    </tr>
    <tr>
      <th>278</th>
      <td>El Monte</td>
      <td>91733</td>
    </tr>
    <tr>
      <th>279</th>
      <td>Whittier</td>
      <td>90601</td>
    </tr>
    <tr>
      <th>280</th>
      <td>Whittier</td>
      <td>90602</td>
    </tr>
    <tr>
      <th>281</th>
      <td>Whittier</td>
      <td>90603</td>
    </tr>
    <tr>
      <th>282</th>
      <td>Whittier</td>
      <td>90604</td>
    </tr>
    <tr>
      <th>283</th>
      <td>Whittier</td>
      <td>90605</td>
    </tr>
    <tr>
      <th>284</th>
      <td>Whittier</td>
      <td>90606</td>
    </tr>
    <tr>
      <th>285</th>
      <td>Whittier</td>
      <td>90607</td>
    </tr>
    <tr>
      <th>286</th>
      <td>Whittier</td>
      <td>90608</td>
    </tr>
    <tr>
      <th>287</th>
      <td>Whittier</td>
      <td>90609</td>
    </tr>
    <tr>
      <th>288</th>
      <td>Whittier</td>
      <td>90610</td>
    </tr>
    <tr>
      <th>289</th>
      <td>Whittier</td>
      <td>90612</td>
    </tr>
    <tr>
      <th>290</th>
      <td>Alhambra</td>
      <td>91801</td>
    </tr>
    <tr>
      <th>291</th>
      <td>Alhambra</td>
      <td>91802</td>
    </tr>
    <tr>
      <th>292</th>
      <td>Alhambra</td>
      <td>91803</td>
    </tr>
    <tr>
      <th>293</th>
      <td>Alhambra</td>
      <td>91804</td>
    </tr>
    <tr>
      <th>294</th>
      <td>Alhambra</td>
      <td>91841</td>
    </tr>
    <tr>
      <th>295</th>
      <td>Alhambra</td>
      <td>91896</td>
    </tr>
    <tr>
      <th>296</th>
      <td>Alhambra</td>
      <td>91899</td>
    </tr>
  </tbody>
</table>
<p>297 rows × 2 columns</p>
</div>


#### 2.Google_Search_Airport_Park_Transportation_Mall_By_City

```python
#Using Google Search to obtain closest amenities by cities
# code by Sue Del Carpio Bellido

# Dependencies
import requests
import json
import pandas as pd


# Google developer API key
from config import gkey_places

file_one = "../Raw_Data/1-1.LA_cities_Lat_lng_codes_data.csv"
cities_tot_df = pd.read_csv(file_one, encoding = "ISO-8859-1")

cities_tot_df = cities_tot_df.rename(columns={"address":"City"})
cities_tot_df

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>lat</th>
      <th>lng</th>
      <th>northeast_Lat</th>
      <th>northeast_Lng</th>
      <th>southwest_Lat</th>
      <th>southwest_Lng</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>34.052234</td>
      <td>-118.243685</td>
      <td>34.337306</td>
      <td>-118.155289</td>
      <td>33.703652</td>
      <td>-118.668176</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>33.770050</td>
      <td>-118.193740</td>
      <td>33.885459</td>
      <td>-118.063253</td>
      <td>33.714957</td>
      <td>-118.248966</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>34.142508</td>
      <td>-118.255075</td>
      <td>34.267232</td>
      <td>-118.182005</td>
      <td>34.118761</td>
      <td>-118.307849</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Lancaster</td>
      <td>40.037875</td>
      <td>-76.305514</td>
      <td>40.073041</td>
      <td>-76.254084</td>
      <td>40.006910</td>
      <td>-76.346614</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>34.579434</td>
      <td>-118.116461</td>
      <td>34.661043</td>
      <td>-117.915747</td>
      <td>34.509813</td>
      <td>-118.287107</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Santa Clarita</td>
      <td>34.391664</td>
      <td>-118.542586</td>
      <td>34.477524</td>
      <td>-118.376071</td>
      <td>34.340498</td>
      <td>-118.613192</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Pomona</td>
      <td>34.055103</td>
      <td>-117.749991</td>
      <td>34.112936</td>
      <td>-117.711067</td>
      <td>34.018512</td>
      <td>-117.828817</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Torrance</td>
      <td>33.835849</td>
      <td>-118.340629</td>
      <td>33.887061</td>
      <td>-118.308127</td>
      <td>33.780217</td>
      <td>-118.394091</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Pasadena</td>
      <td>34.147785</td>
      <td>-118.144515</td>
      <td>34.251905</td>
      <td>-118.065479</td>
      <td>34.117037</td>
      <td>-118.198139</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Inglewood</td>
      <td>33.961680</td>
      <td>-118.353131</td>
      <td>33.982970</td>
      <td>-118.313391</td>
      <td>33.925177</td>
      <td>-118.378850</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Compton</td>
      <td>33.895849</td>
      <td>-118.220071</td>
      <td>33.923418</td>
      <td>-118.179962</td>
      <td>33.863086</td>
      <td>-118.263659</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Downey</td>
      <td>33.940109</td>
      <td>-118.133159</td>
      <td>33.972899</td>
      <td>-118.090262</td>
      <td>33.902455</td>
      <td>-118.170584</td>
    </tr>
    <tr>
      <th>12</th>
      <td>West Covina</td>
      <td>34.068621</td>
      <td>-117.938953</td>
      <td>34.092493</td>
      <td>-117.858261</td>
      <td>34.001855</td>
      <td>-117.967138</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Norwalk</td>
      <td>41.117744</td>
      <td>-73.408158</td>
      <td>41.171596</td>
      <td>-73.380562</td>
      <td>41.020449</td>
      <td>-73.474565</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burbank</td>
      <td>34.180839</td>
      <td>-118.308966</td>
      <td>34.221654</td>
      <td>-118.280109</td>
      <td>34.142367</td>
      <td>-118.370313</td>
    </tr>
    <tr>
      <th>15</th>
      <td>South Gate</td>
      <td>33.954737</td>
      <td>-118.212016</td>
      <td>33.966353</td>
      <td>-118.156119</td>
      <td>33.909964</td>
      <td>-118.231505</td>
    </tr>
    <tr>
      <th>16</th>
      <td>El Monte</td>
      <td>34.068621</td>
      <td>-118.027567</td>
      <td>34.100946</td>
      <td>-117.997465</td>
      <td>34.041393</td>
      <td>-118.072927</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Whittier</td>
      <td>33.979179</td>
      <td>-118.032844</td>
      <td>34.030716</td>
      <td>-117.965576</td>
      <td>33.928167</td>
      <td>-118.072246</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alhambra</td>
      <td>34.095287</td>
      <td>-118.127015</td>
      <td>34.111146</td>
      <td>-118.108181</td>
      <td>34.059921</td>
      <td>-118.164835</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Filter only selected cities for analysis
selected_cities=['Alhambra','Burbank','Inglewood','Glendale','Long Beach','Los Angeles','Palmdale','Pasadena','Santa Clarita','Torrance']
cities_df=cities_tot_df[cities_tot_df['City'].isin(selected_cities)]
cities_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>lat</th>
      <th>lng</th>
      <th>northeast_Lat</th>
      <th>northeast_Lng</th>
      <th>southwest_Lat</th>
      <th>southwest_Lng</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>34.052234</td>
      <td>-118.243685</td>
      <td>34.337306</td>
      <td>-118.155289</td>
      <td>33.703652</td>
      <td>-118.668176</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>33.770050</td>
      <td>-118.193740</td>
      <td>33.885459</td>
      <td>-118.063253</td>
      <td>33.714957</td>
      <td>-118.248966</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>34.142508</td>
      <td>-118.255075</td>
      <td>34.267232</td>
      <td>-118.182005</td>
      <td>34.118761</td>
      <td>-118.307849</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>34.579434</td>
      <td>-118.116461</td>
      <td>34.661043</td>
      <td>-117.915747</td>
      <td>34.509813</td>
      <td>-118.287107</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Santa Clarita</td>
      <td>34.391664</td>
      <td>-118.542586</td>
      <td>34.477524</td>
      <td>-118.376071</td>
      <td>34.340498</td>
      <td>-118.613192</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Torrance</td>
      <td>33.835849</td>
      <td>-118.340629</td>
      <td>33.887061</td>
      <td>-118.308127</td>
      <td>33.780217</td>
      <td>-118.394091</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Pasadena</td>
      <td>34.147785</td>
      <td>-118.144515</td>
      <td>34.251905</td>
      <td>-118.065479</td>
      <td>34.117037</td>
      <td>-118.198139</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Inglewood</td>
      <td>33.961680</td>
      <td>-118.353131</td>
      <td>33.982970</td>
      <td>-118.313391</td>
      <td>33.925177</td>
      <td>-118.378850</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burbank</td>
      <td>34.180839</td>
      <td>-118.308966</td>
      <td>34.221654</td>
      <td>-118.280109</td>
      <td>34.142367</td>
      <td>-118.370313</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alhambra</td>
      <td>34.095287</td>
      <td>-118.127015</td>
      <td>34.111146</td>
      <td>-118.108181</td>
      <td>34.059921</td>
      <td>-118.164835</td>
    </tr>
  </tbody>
</table>
</div>




```python
# AIRPORTS close to cities
cities_df["airport"]=None

base_url = "https://maps.googleapis.com/maps/api/place/nearbysearch/json"

for index, row in cities_df.iterrows():
    target_coordinates = str(row["lat"]) +","+str(row["lng"]) 
    target_radius = 5000
    target_type = "airport"
    #target_keyword ="airport"

    params = {
        "location": target_coordinates,
        "radius": target_radius,
        "type": target_type,
        "key": gkey_places}
        #"keyword": target_keyword}

    response = requests.get(base_url, params=params)
    airport_data = response.json()

    #print(json.dumps(airport_data, indent=4, sort_keys=True))

    counter = 0
    for airport in airport_data["results"]:
        #print(airport["name"])
        #print(airport["vicinity"])
        #print(airport["name"].upper().find("AIRPORT"))
        
        if airport["name"].upper().find("AIRPORT")>0:
            counter += 1
            
        
    cities_df.set_value(index,"airport",counter)
cities_df
```

    C:\Users\liang\Anaconda3\envs\pydata\lib\site-packages\ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>lat</th>
      <th>lng</th>
      <th>northeast_Lat</th>
      <th>northeast_Lng</th>
      <th>southwest_Lat</th>
      <th>southwest_Lng</th>
      <th>public_transportation</th>
      <th>park</th>
      <th>shopping_mall</th>
      <th>airport</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>34.052234</td>
      <td>-118.243685</td>
      <td>34.337306</td>
      <td>-118.155289</td>
      <td>33.703652</td>
      <td>-118.668176</td>
      <td>19</td>
      <td>16</td>
      <td>11</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>33.770050</td>
      <td>-118.193740</td>
      <td>33.885459</td>
      <td>-118.063253</td>
      <td>33.714957</td>
      <td>-118.248966</td>
      <td>8</td>
      <td>15</td>
      <td>13</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>34.142508</td>
      <td>-118.255075</td>
      <td>34.267232</td>
      <td>-118.182005</td>
      <td>34.118761</td>
      <td>-118.307849</td>
      <td>4</td>
      <td>16</td>
      <td>11</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>34.579434</td>
      <td>-118.116461</td>
      <td>34.661043</td>
      <td>-117.915747</td>
      <td>34.509813</td>
      <td>-118.287107</td>
      <td>0</td>
      <td>20</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Santa Clarita</td>
      <td>34.391664</td>
      <td>-118.542586</td>
      <td>34.477524</td>
      <td>-118.376071</td>
      <td>34.340498</td>
      <td>-118.613192</td>
      <td>0</td>
      <td>14</td>
      <td>12</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Torrance</td>
      <td>33.835849</td>
      <td>-118.340629</td>
      <td>33.887061</td>
      <td>-118.308127</td>
      <td>33.780217</td>
      <td>-118.394091</td>
      <td>1</td>
      <td>15</td>
      <td>12</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Pasadena</td>
      <td>34.147785</td>
      <td>-118.144515</td>
      <td>34.251905</td>
      <td>-118.065479</td>
      <td>34.117037</td>
      <td>-118.198139</td>
      <td>9</td>
      <td>15</td>
      <td>10</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Inglewood</td>
      <td>33.961680</td>
      <td>-118.353131</td>
      <td>33.982970</td>
      <td>-118.313391</td>
      <td>33.925177</td>
      <td>-118.378850</td>
      <td>11</td>
      <td>16</td>
      <td>11</td>
      <td>4</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burbank</td>
      <td>34.180839</td>
      <td>-118.308966</td>
      <td>34.221654</td>
      <td>-118.280109</td>
      <td>34.142367</td>
      <td>-118.370313</td>
      <td>0</td>
      <td>16</td>
      <td>9</td>
      <td>2</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alhambra</td>
      <td>34.095287</td>
      <td>-118.127015</td>
      <td>34.111146</td>
      <td>-118.108181</td>
      <td>34.059921</td>
      <td>-118.164835</td>
      <td>13</td>
      <td>14</td>
      <td>8</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# PUBLIC TRANSPORTATION close to cities
cities_df["public_transportation"]=None

base_url = "https://maps.googleapis.com/maps/api/place/nearbysearch/json"

for index, row in cities_df.iterrows():
    target_coordinates = str(row["lat"]) +","+str(row["lng"]) 
    target_radius = 8000
    target_type = ["light_rail_station",
                "transit_station","subway_station"]
    #target_keyword ="bank"

    params = {
        "location": target_coordinates,
        "radius": target_radius,
        "type": target_type,
        "key": gkey_places}
        #"keyword": target_keyword}

    response = requests.get(base_url, params=params)
    train_data = response.json()

    #print(json.dumps(train_data, indent=4, sort_keys=True))

    counter = 0
    for train in train_data["results"]:
        #print(train["name"])
        #print(train["vicinity"])
        counter += 1
        
    cities_df.set_value(index,"public_transportation",counter)
cities_df
```

    C:\Users\liang\Anaconda3\envs\pydata\lib\site-packages\ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>lat</th>
      <th>lng</th>
      <th>northeast_Lat</th>
      <th>northeast_Lng</th>
      <th>southwest_Lat</th>
      <th>southwest_Lng</th>
      <th>public_transportation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>34.052234</td>
      <td>-118.243685</td>
      <td>34.337306</td>
      <td>-118.155289</td>
      <td>33.703652</td>
      <td>-118.668176</td>
      <td>19</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>33.770050</td>
      <td>-118.193740</td>
      <td>33.885459</td>
      <td>-118.063253</td>
      <td>33.714957</td>
      <td>-118.248966</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>34.142508</td>
      <td>-118.255075</td>
      <td>34.267232</td>
      <td>-118.182005</td>
      <td>34.118761</td>
      <td>-118.307849</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>34.579434</td>
      <td>-118.116461</td>
      <td>34.661043</td>
      <td>-117.915747</td>
      <td>34.509813</td>
      <td>-118.287107</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Santa Clarita</td>
      <td>34.391664</td>
      <td>-118.542586</td>
      <td>34.477524</td>
      <td>-118.376071</td>
      <td>34.340498</td>
      <td>-118.613192</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Torrance</td>
      <td>33.835849</td>
      <td>-118.340629</td>
      <td>33.887061</td>
      <td>-118.308127</td>
      <td>33.780217</td>
      <td>-118.394091</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Pasadena</td>
      <td>34.147785</td>
      <td>-118.144515</td>
      <td>34.251905</td>
      <td>-118.065479</td>
      <td>34.117037</td>
      <td>-118.198139</td>
      <td>9</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Inglewood</td>
      <td>33.961680</td>
      <td>-118.353131</td>
      <td>33.982970</td>
      <td>-118.313391</td>
      <td>33.925177</td>
      <td>-118.378850</td>
      <td>11</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burbank</td>
      <td>34.180839</td>
      <td>-118.308966</td>
      <td>34.221654</td>
      <td>-118.280109</td>
      <td>34.142367</td>
      <td>-118.370313</td>
      <td>0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alhambra</td>
      <td>34.095287</td>
      <td>-118.127015</td>
      <td>34.111146</td>
      <td>-118.108181</td>
      <td>34.059921</td>
      <td>-118.164835</td>
      <td>13</td>
    </tr>
  </tbody>
</table>
</div>




```python
# PARKS close to cities
cities_df["park"]=None

base_url = "https://maps.googleapis.com/maps/api/place/nearbysearch/json"

for index, row in cities_df.iterrows():
    target_coordinates = str(row["lat"]) +","+str(row["lng"]) 
    target_radius = 8000
    target_type = "park"
    #target_keyword ="bank"

    params = {
        "location": target_coordinates,
        "radius": target_radius,
        "type": target_type,
        "key": gkey_places}
        #"keyword": target_keyword}

    response = requests.get(base_url, params=params)
    park_data = response.json()

    #print(json.dumps(park_data, indent=4, sort_keys=True))

    counter = 0
    for park in park_data["results"]:
        #print(park["name"])
        #print(park["vicinity"])
        #print(park["rating"])
        #if park["rating"]>3:
        counter += 1
                
    cities_df.set_value(index,"park",counter)
cities_df
```

    C:\Users\liang\Anaconda3\envs\pydata\lib\site-packages\ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>lat</th>
      <th>lng</th>
      <th>northeast_Lat</th>
      <th>northeast_Lng</th>
      <th>southwest_Lat</th>
      <th>southwest_Lng</th>
      <th>public_transportation</th>
      <th>park</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>34.052234</td>
      <td>-118.243685</td>
      <td>34.337306</td>
      <td>-118.155289</td>
      <td>33.703652</td>
      <td>-118.668176</td>
      <td>19</td>
      <td>16</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>33.770050</td>
      <td>-118.193740</td>
      <td>33.885459</td>
      <td>-118.063253</td>
      <td>33.714957</td>
      <td>-118.248966</td>
      <td>8</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>34.142508</td>
      <td>-118.255075</td>
      <td>34.267232</td>
      <td>-118.182005</td>
      <td>34.118761</td>
      <td>-118.307849</td>
      <td>4</td>
      <td>16</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>34.579434</td>
      <td>-118.116461</td>
      <td>34.661043</td>
      <td>-117.915747</td>
      <td>34.509813</td>
      <td>-118.287107</td>
      <td>0</td>
      <td>20</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Santa Clarita</td>
      <td>34.391664</td>
      <td>-118.542586</td>
      <td>34.477524</td>
      <td>-118.376071</td>
      <td>34.340498</td>
      <td>-118.613192</td>
      <td>0</td>
      <td>14</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Torrance</td>
      <td>33.835849</td>
      <td>-118.340629</td>
      <td>33.887061</td>
      <td>-118.308127</td>
      <td>33.780217</td>
      <td>-118.394091</td>
      <td>1</td>
      <td>15</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Pasadena</td>
      <td>34.147785</td>
      <td>-118.144515</td>
      <td>34.251905</td>
      <td>-118.065479</td>
      <td>34.117037</td>
      <td>-118.198139</td>
      <td>9</td>
      <td>15</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Inglewood</td>
      <td>33.961680</td>
      <td>-118.353131</td>
      <td>33.982970</td>
      <td>-118.313391</td>
      <td>33.925177</td>
      <td>-118.378850</td>
      <td>11</td>
      <td>16</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burbank</td>
      <td>34.180839</td>
      <td>-118.308966</td>
      <td>34.221654</td>
      <td>-118.280109</td>
      <td>34.142367</td>
      <td>-118.370313</td>
      <td>0</td>
      <td>16</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alhambra</td>
      <td>34.095287</td>
      <td>-118.127015</td>
      <td>34.111146</td>
      <td>-118.108181</td>
      <td>34.059921</td>
      <td>-118.164835</td>
      <td>13</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>




```python
# SHOPPING MALLS close to cities
cities_df["shopping_mall"]=None

base_url = "https://maps.googleapis.com/maps/api/place/nearbysearch/json"

for index, row in cities_df.iterrows():
    target_coordinates = str(row["lat"]) +","+str(row["lng"]) 
    target_radius = 5000
    target_type = "shopping_mall"
    #target_keyword ="bank"

    params = {
        "location": target_coordinates,
        "radius": target_radius,
        "type": target_type,
        "key": gkey_places}
        #"keyword": target_keyword}

    response = requests.get(base_url, params=params)
    shopping_mall_data = response.json()

    #print(json.dumps(shopping_mall_data, indent=4, sort_keys=True))

    counter = 0
    for shopping_mall in shopping_mall_data["results"]:
        #print(shopping_mall["name"])
        #print(shopping_mall["vicinity"])
        #print(shopping_mall["rating"])
        
        try:
            if shopping_mall["rating"]>4:
                counter += 1
        except KeyError:
            continue
        
                
    cities_df.set_value(index,"shopping_mall",counter)
cities_df.head()
```

    C:\Users\liang\Anaconda3\envs\pydata\lib\site-packages\ipykernel_launcher.py:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>lat</th>
      <th>lng</th>
      <th>northeast_Lat</th>
      <th>northeast_Lng</th>
      <th>southwest_Lat</th>
      <th>southwest_Lng</th>
      <th>public_transportation</th>
      <th>park</th>
      <th>shopping_mall</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>34.052234</td>
      <td>-118.243685</td>
      <td>34.337306</td>
      <td>-118.155289</td>
      <td>33.703652</td>
      <td>-118.668176</td>
      <td>19</td>
      <td>16</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>33.770050</td>
      <td>-118.193740</td>
      <td>33.885459</td>
      <td>-118.063253</td>
      <td>33.714957</td>
      <td>-118.248966</td>
      <td>8</td>
      <td>15</td>
      <td>13</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>34.142508</td>
      <td>-118.255075</td>
      <td>34.267232</td>
      <td>-118.182005</td>
      <td>34.118761</td>
      <td>-118.307849</td>
      <td>4</td>
      <td>16</td>
      <td>11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>34.579434</td>
      <td>-118.116461</td>
      <td>34.661043</td>
      <td>-117.915747</td>
      <td>34.509813</td>
      <td>-118.287107</td>
      <td>0</td>
      <td>20</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Santa Clarita</td>
      <td>34.391664</td>
      <td>-118.542586</td>
      <td>34.477524</td>
      <td>-118.376071</td>
      <td>34.340498</td>
      <td>-118.613192</td>
      <td>0</td>
      <td>14</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Visualize the DataFrame
cities_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>lat</th>
      <th>lng</th>
      <th>northeast_Lat</th>
      <th>northeast_Lng</th>
      <th>southwest_Lat</th>
      <th>southwest_Lng</th>
      <th>public_transportation</th>
      <th>park</th>
      <th>shopping_mall</th>
      <th>airport</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>34.052234</td>
      <td>-118.243685</td>
      <td>34.337306</td>
      <td>-118.155289</td>
      <td>33.703652</td>
      <td>-118.668176</td>
      <td>19</td>
      <td>16</td>
      <td>11</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>33.770050</td>
      <td>-118.193740</td>
      <td>33.885459</td>
      <td>-118.063253</td>
      <td>33.714957</td>
      <td>-118.248966</td>
      <td>8</td>
      <td>15</td>
      <td>13</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>34.142508</td>
      <td>-118.255075</td>
      <td>34.267232</td>
      <td>-118.182005</td>
      <td>34.118761</td>
      <td>-118.307849</td>
      <td>4</td>
      <td>16</td>
      <td>11</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>34.579434</td>
      <td>-118.116461</td>
      <td>34.661043</td>
      <td>-117.915747</td>
      <td>34.509813</td>
      <td>-118.287107</td>
      <td>0</td>
      <td>20</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Santa Clarita</td>
      <td>34.391664</td>
      <td>-118.542586</td>
      <td>34.477524</td>
      <td>-118.376071</td>
      <td>34.340498</td>
      <td>-118.613192</td>
      <td>0</td>
      <td>14</td>
      <td>12</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Torrance</td>
      <td>33.835849</td>
      <td>-118.340629</td>
      <td>33.887061</td>
      <td>-118.308127</td>
      <td>33.780217</td>
      <td>-118.394091</td>
      <td>1</td>
      <td>15</td>
      <td>12</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Pasadena</td>
      <td>34.147785</td>
      <td>-118.144515</td>
      <td>34.251905</td>
      <td>-118.065479</td>
      <td>34.117037</td>
      <td>-118.198139</td>
      <td>9</td>
      <td>15</td>
      <td>10</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Inglewood</td>
      <td>33.961680</td>
      <td>-118.353131</td>
      <td>33.982970</td>
      <td>-118.313391</td>
      <td>33.925177</td>
      <td>-118.378850</td>
      <td>11</td>
      <td>16</td>
      <td>11</td>
      <td>4</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burbank</td>
      <td>34.180839</td>
      <td>-118.308966</td>
      <td>34.221654</td>
      <td>-118.280109</td>
      <td>34.142367</td>
      <td>-118.370313</td>
      <td>0</td>
      <td>16</td>
      <td>9</td>
      <td>2</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Alhambra</td>
      <td>34.095287</td>
      <td>-118.127015</td>
      <td>34.111146</td>
      <td>-118.108181</td>
      <td>34.059921</td>
      <td>-118.164835</td>
      <td>13</td>
      <td>14</td>
      <td>8</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
cities_dfb=cities_df[['City','public_transportation','park','shopping_mall','airport']]
cities_dfb.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>public_transportation</th>
      <th>park</th>
      <th>shopping_mall</th>
      <th>airport</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>19</td>
      <td>16</td>
      <td>11</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Long Beach</td>
      <td>8</td>
      <td>15</td>
      <td>13</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>4</td>
      <td>16</td>
      <td>11</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Palmdale</td>
      <td>0</td>
      <td>20</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Santa Clarita</td>
      <td>0</td>
      <td>14</td>
      <td>12</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
##Unpivot data for Seaborn plots
##Code by Lindsay Yang
cities_dfc=pd.melt(cities_dfb, id_vars=['City'], value_vars=['public_transportation', 'park','shopping_mall','airport'])
```


```python
cities=cities_dfb[['City']]
```


```python
import seaborn as sns
import matplotlib.pyplot as plt


sns.set_style("whitegrid")
plt.figure(figsize=(20,8))
sns.barplot(x='City', y='value', hue='variable', data=cities_dfc)
plt.xticks(rotation=90)

plt.ylabel('count of amenities')
plt.title('Amenities in LA cities')
plt.show()

# Save the figure
plt.savefig("../Clean_Data/2.Amenities_by_city.png")
```


    <matplotlib.figure.Figure at 0x24c8c9983c8>



![png](Clean_Data/2.Amenities_by_city.png)

#### 3.Pyitup_Census_Analysis



```python
#Using Census API to obtain information of interest to choose a city when buying a property
# code by Sue Del Carpio Bellido

# Dependencies
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import requests

# please download census wrapper from https://pypi.python.org/pypi/census
from census import Census
import seaborn as sns

# Census API Key
from config import api_key

c = Census(api_key, year=2016)
```


```python
zipcodes_df = pd.read_csv("../Raw_Data/1-2.zipcodes_in_LA_counties.csv")

zipcodes_df = zipcodes_df.rename(columns={"zip": "Zipcode","County":"City"})

zipcodes_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Zipcode</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>90001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Los Angeles</td>
      <td>90002</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Los Angeles</td>
      <td>90003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Los Angeles</td>
      <td>90004</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Los Angeles</td>
      <td>90005</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Filter only selected cities for analysis
selected_cities=['Alhambra','Burbank','Inglewood','Glendale','Long Beach','Los Angeles','Palmdale','Pasadena','Santa Clarita','Torrance']
zipcodes_df=zipcodes_df[zipcodes_df['City'].isin(selected_cities)]
zipcodes_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Zipcode</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Los Angeles</td>
      <td>90001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Los Angeles</td>
      <td>90002</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Los Angeles</td>
      <td>90003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Los Angeles</td>
      <td>90004</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Los Angeles</td>
      <td>90005</td>
    </tr>
  </tbody>
</table>
</div>




```python
##Due to Timeout error, we need to call the API 3 times to obtain all information required

census_data = c.acs5.get(("NAME", "B19013_001E", "B01003_001E", "B01002_001E","B19301_001E","B17001_002E",
                            "B23025_004E","B23025_002E","B23025_005E"),{'for': 'zip code tabulation area:*'})

census_pd = pd.DataFrame(census_data)

census_pd = census_pd.rename(columns={"B01003_001E": "Population",
                                      "B01002_001E": "Median Age",
                                      "B19013_001E": "Household Income",
                                      "B19301_001E": "Per Capita Income",
                                      "B17001_002E": "Poverty Count",
                                      "B23025_004E": "employment_employed",
                                      "B23025_002E": "Labor_force",
                                      "B23025_005E": "employment_unemployed",
                                      "NAME": "Name", "zip code tabulation area": "Zipcode"})

# Add in Poverty Rate (Poverty Count / Population)
census_pd["Poverty Rate"] = 100 * \
    census_pd["Poverty Count"].astype(
        int) / census_pd["Population"].astype(int)

# Add in Poverty Rate (Poverty Count / Population)
census_pd["Employment Rate"] = 100 * \
    census_pd["employment_employed"].astype(
        int) / census_pd["Labor_force"].astype(int)
    
# Add in Poverty Rate (Poverty Count / Population)
census_pd["Unemployment Rate"] = 100 * \
    census_pd["employment_unemployed"].astype(
        int) / census_pd["Labor_force"].astype(int)
    
#Final DataFrame
census_pd = census_pd[["Zipcode", "Population", "Median Age", "Household Income",
                       "Per Capita Income", "Poverty Count", "Poverty Rate","employment_employed","Labor_force","employment_unemployed",
                      "Employment Rate", "Unemployment Rate"]]

# Visualize
print(len(census_pd))
census_pd.head()
```

    33120
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Zipcode</th>
      <th>Population</th>
      <th>Median Age</th>
      <th>Household Income</th>
      <th>Per Capita Income</th>
      <th>Poverty Count</th>
      <th>Poverty Rate</th>
      <th>employment_employed</th>
      <th>Labor_force</th>
      <th>employment_unemployed</th>
      <th>Employment Rate</th>
      <th>Unemployment Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01001</td>
      <td>17423.0</td>
      <td>45.0</td>
      <td>56714.0</td>
      <td>30430.0</td>
      <td>1462.0</td>
      <td>8.391207</td>
      <td>8715.0</td>
      <td>9211.0</td>
      <td>479.0</td>
      <td>94.615134</td>
      <td>5.200304</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01002</td>
      <td>29970.0</td>
      <td>23.2</td>
      <td>48923.0</td>
      <td>26072.0</td>
      <td>8351.0</td>
      <td>27.864531</td>
      <td>15180.0</td>
      <td>16451.0</td>
      <td>1271.0</td>
      <td>92.274026</td>
      <td>7.725974</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01003</td>
      <td>11296.0</td>
      <td>19.9</td>
      <td>2499.0</td>
      <td>3829.0</td>
      <td>54.0</td>
      <td>0.478045</td>
      <td>4258.0</td>
      <td>5279.0</td>
      <td>1021.0</td>
      <td>80.659216</td>
      <td>19.340784</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01005</td>
      <td>5228.0</td>
      <td>44.1</td>
      <td>70568.0</td>
      <td>32169.0</td>
      <td>230.0</td>
      <td>4.399388</td>
      <td>2835.0</td>
      <td>2988.0</td>
      <td>153.0</td>
      <td>94.879518</td>
      <td>5.120482</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01007</td>
      <td>14888.0</td>
      <td>42.5</td>
      <td>80502.0</td>
      <td>36359.0</td>
      <td>1410.0</td>
      <td>9.470715</td>
      <td>8050.0</td>
      <td>8593.0</td>
      <td>543.0</td>
      <td>93.680903</td>
      <td>6.319097</td>
    </tr>
  </tbody>
</table>
</div>




```python
census_data_2 = c.acs5.get(("NAME", "B01002_002E", "B01002_003E", "B08136_011E","B15003_002E","B01001_002E",
                            "B01001_026E"),{'for': 'zip code tabulation area:*'})

census_pd_2 = pd.DataFrame(census_data_2)

census_pd_2 = census_pd_2.rename(columns={"B01002_002E": "Median_male_age",
                                      "B01002_003E": "Median_female_age",
                                      "B08136_011E": "Walkable_time_min", 
                                      "B15003_002E": "Education_none",
                                      "B01001_002E": "Male_population",
                                      "B01001_026E": "Female_population",
                                      "NAME": "Name", "zip code tabulation area": "Zipcode"})

#Final DataFrame
census_pd_2 = census_pd_2[["Zipcode", "Median_male_age", "Median_female_age", "Walkable_time_min","Education_none", 
                           "Male_population", "Female_population"]]

# Visualize
print(len(census_pd_2))
census_pd_2.head()
```

    33120
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Zipcode</th>
      <th>Median_male_age</th>
      <th>Median_female_age</th>
      <th>Walkable_time_min</th>
      <th>Education_none</th>
      <th>Male_population</th>
      <th>Female_population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01001</td>
      <td>41.6</td>
      <td>48.1</td>
      <td>NaN</td>
      <td>69.0</td>
      <td>8059.0</td>
      <td>9364.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01002</td>
      <td>23.3</td>
      <td>23.2</td>
      <td>19100.0</td>
      <td>212.0</td>
      <td>14536.0</td>
      <td>15434.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01003</td>
      <td>19.9</td>
      <td>19.9</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>5694.0</td>
      <td>5602.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01005</td>
      <td>41.6</td>
      <td>47.4</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>2798.0</td>
      <td>2430.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01007</td>
      <td>40.2</td>
      <td>43.8</td>
      <td>NaN</td>
      <td>18.0</td>
      <td>7224.0</td>
      <td>7664.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
census_data_3 = c.acs5.get(("NAME", "B14002_001E", "B16003_002E", "B16003_008E","B19083_001E"),{'for': 'zip code tabulation area:*'})

# Convert to DataFrame
census_pd_3 = pd.DataFrame(census_data_3)

# Column Reordering
census_pd_3 = census_pd_3.rename(columns={"B14002_001E": "Students_population",
                                       "B16003_002E": "Population_from_5_17",
                                       "B16003_008E": "Population_18_over",
                                       "B19083_001E": "Gini_index",
                                      "NAME": "Name", "zip code tabulation area": "Zipcode"})
    
#Final DataFrame
census_pd_3 = census_pd_3[["Zipcode", "Students_population", "Population_from_5_17", "Population_18_over","Gini_index"]]
                        
# Visualize
print(len(census_pd_3))
census_pd_3.head()
```

    33120
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Zipcode</th>
      <th>Students_population</th>
      <th>Population_from_5_17</th>
      <th>Population_18_over</th>
      <th>Gini_index</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01001</td>
      <td>17029.0</td>
      <td>14.0</td>
      <td>153.0</td>
      <td>0.4052</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01002</td>
      <td>29476.0</td>
      <td>71.0</td>
      <td>564.0</td>
      <td>0.5258</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01003</td>
      <td>11296.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.5861</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01005</td>
      <td>5156.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.4053</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01007</td>
      <td>14518.0</td>
      <td>9.0</td>
      <td>263.0</td>
      <td>0.4300</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge two dataframes using an inner join
merge_table_1 = pd.merge(census_pd, census_pd_2, on="Zipcode")
merge_table_1.head()
print(len(merge_table_1))
```

    33120
    


```python
# Merge two dataframes using an inner join
merge_table_total = pd.merge(merge_table_1, census_pd_3, on="Zipcode")
merge_table_total.head()
#print(len(merge_table_total))
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Zipcode</th>
      <th>Population</th>
      <th>Median Age</th>
      <th>Household Income</th>
      <th>Per Capita Income</th>
      <th>Poverty Count</th>
      <th>Poverty Rate</th>
      <th>employment_employed</th>
      <th>Labor_force</th>
      <th>employment_unemployed</th>
      <th>...</th>
      <th>Median_male_age</th>
      <th>Median_female_age</th>
      <th>Walkable_time_min</th>
      <th>Education_none</th>
      <th>Male_population</th>
      <th>Female_population</th>
      <th>Students_population</th>
      <th>Population_from_5_17</th>
      <th>Population_18_over</th>
      <th>Gini_index</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>01001</td>
      <td>17423.0</td>
      <td>45.0</td>
      <td>56714.0</td>
      <td>30430.0</td>
      <td>1462.0</td>
      <td>8.391207</td>
      <td>8715.0</td>
      <td>9211.0</td>
      <td>479.0</td>
      <td>...</td>
      <td>41.6</td>
      <td>48.1</td>
      <td>NaN</td>
      <td>69.0</td>
      <td>8059.0</td>
      <td>9364.0</td>
      <td>17029.0</td>
      <td>14.0</td>
      <td>153.0</td>
      <td>0.4052</td>
    </tr>
    <tr>
      <th>1</th>
      <td>01002</td>
      <td>29970.0</td>
      <td>23.2</td>
      <td>48923.0</td>
      <td>26072.0</td>
      <td>8351.0</td>
      <td>27.864531</td>
      <td>15180.0</td>
      <td>16451.0</td>
      <td>1271.0</td>
      <td>...</td>
      <td>23.3</td>
      <td>23.2</td>
      <td>19100.0</td>
      <td>212.0</td>
      <td>14536.0</td>
      <td>15434.0</td>
      <td>29476.0</td>
      <td>71.0</td>
      <td>564.0</td>
      <td>0.5258</td>
    </tr>
    <tr>
      <th>2</th>
      <td>01003</td>
      <td>11296.0</td>
      <td>19.9</td>
      <td>2499.0</td>
      <td>3829.0</td>
      <td>54.0</td>
      <td>0.478045</td>
      <td>4258.0</td>
      <td>5279.0</td>
      <td>1021.0</td>
      <td>...</td>
      <td>19.9</td>
      <td>19.9</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>5694.0</td>
      <td>5602.0</td>
      <td>11296.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.5861</td>
    </tr>
    <tr>
      <th>3</th>
      <td>01005</td>
      <td>5228.0</td>
      <td>44.1</td>
      <td>70568.0</td>
      <td>32169.0</td>
      <td>230.0</td>
      <td>4.399388</td>
      <td>2835.0</td>
      <td>2988.0</td>
      <td>153.0</td>
      <td>...</td>
      <td>41.6</td>
      <td>47.4</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>2798.0</td>
      <td>2430.0</td>
      <td>5156.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.4053</td>
    </tr>
    <tr>
      <th>4</th>
      <td>01007</td>
      <td>14888.0</td>
      <td>42.5</td>
      <td>80502.0</td>
      <td>36359.0</td>
      <td>1410.0</td>
      <td>9.470715</td>
      <td>8050.0</td>
      <td>8593.0</td>
      <td>543.0</td>
      <td>...</td>
      <td>40.2</td>
      <td>43.8</td>
      <td>NaN</td>
      <td>18.0</td>
      <td>7224.0</td>
      <td>7664.0</td>
      <td>14518.0</td>
      <td>9.0</td>
      <td>263.0</td>
      <td>0.4300</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
#Export clean data
merge_table_total.to_csv("../Clean_Data/3.total_census.csv", encoding="utf-8", index=False, header=True)
```

# Cleaning Data


```python
#Get only Zipcodes from LA selected cities
import numpy as np
merge_table_total['Zipcode']=merge_table_total['Zipcode'].astype(np.int64)

los_angeles_census_df = pd.merge(merge_table_total, zipcodes_df, on="Zipcode")
los_angeles_census_df.to_csv("../Clean_data/3.los_angeles_census.csv", encoding="utf-8", index=False, header=True)
```


```python
los_angeles_census_df.columns
```




    Index(['Zipcode', 'Population', 'Median Age', 'Household Income',
           'Per Capita Income', 'Poverty Count', 'Poverty Rate',
           'employment_employed', 'Labor_force', 'employment_unemployed',
           'Employment Rate', 'Unemployment Rate', 'Median_male_age',
           'Median_female_age', 'Walkable_time_min', 'Education_none',
           'Male_population', 'Female_population', 'Students_population',
           'Population_from_5_17', 'Population_18_over', 'Gini_index', 'City'],
          dtype='object')




```python
# Dropping results with population=0
population_greater_0 = los_angeles_census_df["Population"]>0
los_angeles_census_df=los_angeles_census_df[population_greater_0]
```


```python
##We found default value in census is "-666666666"
##We are going to filter this data for each analysis


#Group by City, aggregation average by Gini index
gini_index_value = los_angeles_census_df["Gini_index"]>-666666666
gini_index_df = los_angeles_census_df[gini_index_value]

gini_index_df = gini_index_df.groupby(["City"])['Gini_index'].agg(['mean']).sort_index().reset_index()
gini_index_df= gini_index_df.rename(columns={"mean":"Gini_index_avg"})

gini_index_df=gini_index_df.sort_values(by='Gini_index_avg', ascending=False)
gini_index_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Gini_index_avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7</th>
      <td>Pasadena</td>
      <td>0.509271</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Los Angeles</td>
      <td>0.490941</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>0.466180</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Alhambra</td>
      <td>0.451150</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burbank</td>
      <td>0.450520</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Inglewood</td>
      <td>0.437020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Long Beach</td>
      <td>0.432907</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Torrance</td>
      <td>0.427600</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Palmdale</td>
      <td>0.407150</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Santa Clarita</td>
      <td>0.395511</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Plot with seaborn, make additional changes with matplotlib
#Palette color reflects values from negative to positive for better understand

sns.set_style("whitegrid")
plt.figure(figsize=(15,7))
sns.barplot(x="City", y="Gini_index_avg", data=gini_index_df, palette=sns.color_palette("RdYlGn", 10))

plt.xlabel("")
plt.ylabel("Gini index")
plt.title("Household income distribution (Gini Coefficient)")

plt.show()

# Save the figure
plt.savefig("../Clean_Data/3.Gini_index_by_City.png")
```


![png](Clean_Data/3.Gini_index_by_City.png)



    <matplotlib.figure.Figure at 0x18b9d82dfd0>


# UNEMPLOYMENT AND POVERTY ANALYSIS 


```python
##Clean and preparing data
unemployment_value = los_angeles_census_df["Unemployment Rate"]>-666666666
poverty_value = los_angeles_census_df["Poverty Rate"]>-666666666

poverty_unemployment_df = los_angeles_census_df[unemployment_value & poverty_value]

poverty_unemployment_df = poverty_unemployment_df.groupby(["City"])[['Unemployment Rate','Poverty Rate']].agg(['mean']).sort_index().reset_index()

poverty_unemployment_df.columns = poverty_unemployment_df.columns.droplevel(1)

poverty_unemployment_df= poverty_unemployment_df.rename(columns={"Unemployment Rate":"Unemployment_Rate","Poverty Rate":"Poverty_Rate"})

poverty_unemployment_df

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Unemployment_Rate</th>
      <th>Poverty_Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alhambra</td>
      <td>5.762571</td>
      <td>14.708418</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burbank</td>
      <td>8.814113</td>
      <td>12.450008</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>7.809085</td>
      <td>14.231462</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Inglewood</td>
      <td>12.604107</td>
      <td>21.751611</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Long Beach</td>
      <td>8.892041</td>
      <td>16.633681</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Los Angeles</td>
      <td>10.441077</td>
      <td>23.850274</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Palmdale</td>
      <td>13.823630</td>
      <td>21.388886</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Pasadena</td>
      <td>6.459477</td>
      <td>13.638440</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Santa Clarita</td>
      <td>7.729977</td>
      <td>7.996643</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Torrance</td>
      <td>7.536710</td>
      <td>9.708102</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Plot unemployment rate and poverty rate in two columns to compare results

sns.set()
poverty_unemployment_df = poverty_unemployment_df.set_index('City')

fig = plt.figure(figsize=(15,8)) # Create matplotlib figure

ax = fig.add_subplot(111) # Create matplotlib axes
ax2 = ax.twinx() # Create another axes that shares the same x-axis as a
width = .3

poverty_unemployment_df.Poverty_Rate.plot(kind='bar',color='blue', ax=ax2,width = width,position=0)

poverty_unemployment_df.Unemployment_Rate.plot(kind='bar',color='green',ax=ax,width=width, position=1)
ax.grid(None, axis=1)
ax2.grid(None)

ax.set_ylabel('Unemployment Rate')
ax2.set_ylabel('Poverty Rate')
plt.title("Unemployment and Poverty rate by Cities")
# Save the figure
plt.savefig("../Clean_Data/3.Unemployment_Poverty_rate_by_City.png")
```


![png](Clean_Data/3.Unemployment_Poverty_rate_by_City.png)


# WALKABLE ANALYSIS


```python
##Clean and preparing data
walk_time_value = los_angeles_census_df["Walkable_time_min"]>-666666666
walk_time_value_df = los_angeles_census_df[walk_time_value]

walk_time_value_df = walk_time_value_df.groupby(["City"])['Walkable_time_min'].agg(['sum']).sort_index().reset_index()
walk_time_value_df= walk_time_value_df.rename(columns={"sum":"Walkable_time_min_total"})

walk_time_value_df=walk_time_value_df.sort_values(by='Walkable_time_min_total', ascending=True)
walk_time_value_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Walkable_time_min_total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alhambra</td>
      <td>1775.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Inglewood</td>
      <td>5935.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Palmdale</td>
      <td>5945.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Santa Clarita</td>
      <td>7285.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>10110.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Torrance</td>
      <td>11565.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burbank</td>
      <td>13860.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Pasadena</td>
      <td>40900.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Long Beach</td>
      <td>55145.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Los Angeles</td>
      <td>465885.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.set_style("whitegrid")
plt.figure(figsize=(15,7))
sns.barplot(x="City", y="Walkable_time_min_total", data=walk_time_value_df, palette=sns.color_palette("RdYlGn", 10))

plt.xlabel("")
plt.ylabel("Walk time (min)")
plt.title("Walkable cities in LA County")

# Save the figure
plt.savefig("../Clean_Data/3.Walk_time_by_City.png")
```


![png](Clean_Data/3.Walk_time_by_City.png)



```python
##Same analysis, without LA
selected_cities_no_la=['Alhambra','Burbank','Inglewood','Glendale','Long Beach','Palmdale','Pasadena','Santa Clarita','Torrance']
walk_time_value_no_la_df=walk_time_value_df[walk_time_value_df['City'].isin(selected_cities_no_la)]
walk_time_value_no_la_df

sns.set_style("whitegrid")
plt.figure(figsize=(15,7))
sns.barplot(x="City", y="Walkable_time_min_total", data=walk_time_value_no_la_df, palette=sns.color_palette("RdYlGn", 9))

plt.xlabel("")
plt.ylabel("Walk time (min)")
plt.title("Walkable cities without LA")

# Save the figure
plt.savefig("../Clean_Data/3.Walk_time_by_City_no_la.png")
```


![png](Clean_Data/3.Walk_time_by_City_no_la.png)


# AGE ANALYSIS


```python
##Clean and preparing data
median_age_value = los_angeles_census_df["Median Age"]>-666666666
median_male_age_value = los_angeles_census_df["Median_male_age"]>-666666666
median_female_age_value = los_angeles_census_df["Median_female_age"]>-666666666


age_stats_df = los_angeles_census_df[median_age_value & median_male_age_value & median_female_age_value]
age_stats_df = age_stats_df.groupby(["City"])[['Median Age','Median_male_age','Median_female_age']].agg(['mean']).sort_index().reset_index()
age_stats_df.columns = age_stats_df.columns.droplevel(1)
age_stats_df = age_stats_df.rename(columns={"Median Age":"Median_age"})

age_stats_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Median_age</th>
      <th>Median_male_age</th>
      <th>Median_female_age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alhambra</td>
      <td>41.300000</td>
      <td>38.850000</td>
      <td>43.10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burbank</td>
      <td>39.540000</td>
      <td>38.660000</td>
      <td>40.84</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>40.440000</td>
      <td>38.090000</td>
      <td>41.84</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Inglewood</td>
      <td>33.920000</td>
      <td>32.540000</td>
      <td>35.32</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Long Beach</td>
      <td>36.092857</td>
      <td>35.157143</td>
      <td>37.00</td>
    </tr>
  </tbody>
</table>
</div>




```python
##Unpivot data for Seaborn plots
sns.set_style("whitegrid")
age_stats_df_plot=age_stats_df[['City','Median_age','Median_male_age','Median_female_age']]

age_stats_df_upivot=pd.melt(age_stats_df_plot, id_vars=['City'], value_vars=['Median_age', 'Median_male_age','Median_female_age'])

cities=age_stats_df[['City']]

plt.figure(figsize=(28,10))
sns.barplot(x='City', y='value', hue='variable', data=age_stats_df_upivot)
plt.xticks(rotation=90)

plt.ylabel('age')
plt.title('Population Age by City')
plt.show()

# Save the figure
plt.savefig("../Clean_Data/3.Age_analysis_city.png")
```


![png](Clean_Data/3.Age_analysis_city.png)



    <matplotlib.figure.Figure at 0x18b9d8d7828>


# EDUCATION ANALYSIS


```python
##Clean and preparing data
Education_none_value = los_angeles_census_df["Education_none"]>-666666666

education_df = los_angeles_census_df[Education_none_value]

education_df = education_df.groupby(["City"])[['Education_none','Population']].agg(['sum']).sort_index().reset_index()
education_df.columns = education_df.columns.droplevel(1)

# Add in Education none Rate (Education none Count / Population)
education_df["Education_none_Rate"] = 100 * \
    education_df["Education_none"].astype(
        int) / education_df["Population"].astype(int)
    
education_df=education_df.sort_values(by='Education_none_Rate', ascending=False)
education_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Education_none</th>
      <th>Population</th>
      <th>Education_none_Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alhambra</td>
      <td>3267.0</td>
      <td>84767.0</td>
      <td>3.854094</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Long Beach</td>
      <td>18840.0</td>
      <td>575287.0</td>
      <td>3.274887</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Los Angeles</td>
      <td>68843.0</td>
      <td>2678395.0</td>
      <td>2.570308</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>4844.0</td>
      <td>209444.0</td>
      <td>2.312790</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Inglewood</td>
      <td>2828.0</td>
      <td>135412.0</td>
      <td>2.088441</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Palmdale</td>
      <td>2965.0</td>
      <td>174283.0</td>
      <td>1.701256</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burbank</td>
      <td>1683.0</td>
      <td>108133.0</td>
      <td>1.556417</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Pasadena</td>
      <td>2330.0</td>
      <td>169915.0</td>
      <td>1.371274</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Torrance</td>
      <td>2033.0</td>
      <td>176673.0</td>
      <td>1.150713</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Santa Clarita</td>
      <td>1989.0</td>
      <td>283616.0</td>
      <td>0.701300</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.set_style("whitegrid")
plt.figure(figsize=(15,7))
sns.barplot(x="City", y="Education_none_Rate", data=education_df, palette=sns.color_palette("RdYlGn", 10))

plt.xlabel("")
plt.ylabel("Education none rate")
plt.title("Education none rate by City")

# Save the figure
plt.savefig("../Clean_Data/3.Education_none_by_City.png")
```


![png](Clean_Data/3.Education_none_by_City.png)




#### 4.School_Ranking_Analysis



```python
# Dependencies
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import requests
import seaborn as sns
```


```python
# Ranking is available through website: http://school-ratings.com/counties/Los_Angeles.html no API calls needed
school_csr_df = pd.read_csv("../Raw_Data/4.LA_cities_school_ranking.csv",encoding = "ISO-8859-1")
#zipcodes_df = zipcodes_df.rename(columns={"zip": "Zipcode","County":"City"})

school_csr_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CITY</th>
      <th>SCHOOL_RAW</th>
      <th>SCHOOL</th>
      <th>CSR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alhambra</td>
      <td>Alhambra High CSR rank: 8</td>
      <td>Alhambra High</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alhambra</td>
      <td>Century High CSR rank: 3</td>
      <td>Century High</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alhambra</td>
      <td>Emery Park Elementary CSR rank: 7</td>
      <td>Emery Park Elementary</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alhambra</td>
      <td>Fremont Elementary CSR rank: 5</td>
      <td>Fremont Elementary</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alhambra</td>
      <td>Garfield Elementary CSR rank: 8</td>
      <td>Garfield Elementary</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Filter only selected cities for analysis
selected_cities=['Alhambra','Burbank','Inglewood','Glendale','Long Beach','Los Angeles','Palmdale','Pasadena','Santa Clarita','Torrance']
school_csr_df=school_csr_df[school_csr_df['CITY'].isin(selected_cities)]
school_csr_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CITY</th>
      <th>SCHOOL_RAW</th>
      <th>SCHOOL</th>
      <th>CSR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alhambra</td>
      <td>Alhambra High CSR rank: 8</td>
      <td>Alhambra High</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alhambra</td>
      <td>Century High CSR rank: 3</td>
      <td>Century High</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alhambra</td>
      <td>Emery Park Elementary CSR rank: 7</td>
      <td>Emery Park Elementary</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alhambra</td>
      <td>Fremont Elementary CSR rank: 5</td>
      <td>Fremont Elementary</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alhambra</td>
      <td>Garfield Elementary CSR rank: 8</td>
      <td>Garfield Elementary</td>
      <td>8</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Alhambra</td>
      <td>Granada Elementary CSR rank: 5</td>
      <td>Granada Elementary</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Alhambra</td>
      <td>Alternative Independence High CSR rank: 3</td>
      <td>Alternative Independence High</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Alhambra</td>
      <td>Marguerita Elementary CSR rank: 7</td>
      <td>Marguerita Elementary</td>
      <td>7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Alhambra</td>
      <td>Mark Keppel High CSR rank: 10</td>
      <td>Mark Keppel High</td>
      <td>10</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Alhambra</td>
      <td>Martha Baldwin Elementary CSR rank: 9</td>
      <td>Martha Baldwin Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Alhambra</td>
      <td>Park Elementary CSR rank: 8</td>
      <td>Park Elementary</td>
      <td>8</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Alhambra</td>
      <td>Ramona Elementary CSR rank: 8</td>
      <td>Ramona Elementary</td>
      <td>8</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Alhambra</td>
      <td>William Northrup Elementary CSR rank: 7</td>
      <td>William Northrup Elementary</td>
      <td>7</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Burbank</td>
      <td>Bret Harte Elementary CSR rank: 7</td>
      <td>Bret Harte Elementary</td>
      <td>7</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burbank</td>
      <td>Burbank High CSR rank: 8</td>
      <td>Burbank High</td>
      <td>8</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Burbank</td>
      <td>Burroughs High CSR rank: 9</td>
      <td>Burroughs High</td>
      <td>9</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Burbank</td>
      <td>David Starr Jordan Middle CSR rank: 7</td>
      <td>David Starr Jordan Middle</td>
      <td>7</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Burbank</td>
      <td>George Washington Elementary CSR rank: 8</td>
      <td>George Washington Elementary</td>
      <td>8</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Burbank</td>
      <td>Joaquin Miller Elementary CSR rank: 9</td>
      <td>Joaquin Miller Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Burbank</td>
      <td>John Muir Middle CSR rank: 8</td>
      <td>John Muir Middle</td>
      <td>8</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Burbank</td>
      <td>Luther Burbank Middle CSR rank: 7</td>
      <td>Luther Burbank Middle</td>
      <td>7</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Burbank</td>
      <td>Continuation Monterey High CSR rank: 2</td>
      <td>Continuation Monterey High</td>
      <td>2</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Burbank</td>
      <td>Options for Youth-Burbank Charter CSR rank: 4</td>
      <td>Options for Youth-Burbank Charter</td>
      <td>4</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Burbank</td>
      <td>Providencia Elementary CSR rank: 7</td>
      <td>Providencia Elementary</td>
      <td>7</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Burbank</td>
      <td>R. L. Stevenson Elementary CSR rank: 9</td>
      <td>R. L. Stevenson Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Burbank</td>
      <td>Ralph Emerson Elementary CSR rank: 8</td>
      <td>Ralph Emerson Elementary</td>
      <td>8</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Burbank</td>
      <td>Theodore Roosevelt Elementary CSR rank: 9</td>
      <td>Theodore Roosevelt Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Burbank</td>
      <td>Thomas Edison Elementary CSR rank: 9</td>
      <td>Thomas Edison Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Burbank</td>
      <td>Thomas Jefferson Elementary CSR rank: 9</td>
      <td>Thomas Jefferson Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Burbank</td>
      <td>Walt Disney Elementary CSR rank: 7</td>
      <td>Walt Disney Elementary</td>
      <td>7</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>941</th>
      <td>Torrance</td>
      <td>Anza Elementary CSR rank: 10</td>
      <td>Anza Elementary</td>
      <td>10</td>
    </tr>
    <tr>
      <th>942</th>
      <td>Torrance</td>
      <td>Arlington Elementary CSR rank: 9</td>
      <td>Arlington Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>943</th>
      <td>Torrance</td>
      <td>Bert M. Lynn Middle CSR rank: 10</td>
      <td>Bert M. Lynn Middle</td>
      <td>10</td>
    </tr>
    <tr>
      <th>944</th>
      <td>Torrance</td>
      <td>Calle Mayor Middle CSR rank: 9</td>
      <td>Calle Mayor Middle</td>
      <td>9</td>
    </tr>
    <tr>
      <th>945</th>
      <td>Torrance</td>
      <td>Casimir Middle CSR rank: 8</td>
      <td>Casimir Middle</td>
      <td>8</td>
    </tr>
    <tr>
      <th>946</th>
      <td>Torrance</td>
      <td>Edison Elementary CSR rank: 8</td>
      <td>Edison Elementary</td>
      <td>8</td>
    </tr>
    <tr>
      <th>947</th>
      <td>Torrance</td>
      <td>Edward J. Richardson Middle CSR rank: 10</td>
      <td>Edward J. Richardson Middle</td>
      <td>10</td>
    </tr>
    <tr>
      <th>948</th>
      <td>Torrance</td>
      <td>Evelyn Carr Elementary CSR rank: 7</td>
      <td>Evelyn Carr Elementary</td>
      <td>7</td>
    </tr>
    <tr>
      <th>949</th>
      <td>Torrance</td>
      <td>Fern Elementary CSR rank: 8</td>
      <td>Fern Elementary</td>
      <td>8</td>
    </tr>
    <tr>
      <th>950</th>
      <td>Torrance</td>
      <td>Hickory Elementary CSR rank: 9</td>
      <td>Hickory Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>951</th>
      <td>Torrance</td>
      <td>Howard Wood Elementary CSR rank: 8</td>
      <td>Howard Wood Elementary</td>
      <td>8</td>
    </tr>
    <tr>
      <th>952</th>
      <td>Torrance</td>
      <td>J. H. Hull Middle CSR rank: 6</td>
      <td>J. H. Hull Middle</td>
      <td>6</td>
    </tr>
    <tr>
      <th>953</th>
      <td>Torrance</td>
      <td>Jefferson Middle CSR rank: 9</td>
      <td>Jefferson Middle</td>
      <td>9</td>
    </tr>
    <tr>
      <th>954</th>
      <td>Torrance</td>
      <td>John Adams Elementary CSR rank: 8</td>
      <td>John Adams Elementary</td>
      <td>8</td>
    </tr>
    <tr>
      <th>955</th>
      <td>Torrance</td>
      <td>Joseph Arnold Elementary CSR rank: 9</td>
      <td>Joseph Arnold Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>956</th>
      <td>Torrance</td>
      <td>Lincoln Elementary CSR rank: 8</td>
      <td>Lincoln Elementary</td>
      <td>8</td>
    </tr>
    <tr>
      <th>957</th>
      <td>Torrance</td>
      <td>Madrona Middle CSR rank: 9</td>
      <td>Madrona Middle</td>
      <td>9</td>
    </tr>
    <tr>
      <th>958</th>
      <td>Torrance</td>
      <td>North High CSR rank: 9</td>
      <td>North High</td>
      <td>9</td>
    </tr>
    <tr>
      <th>959</th>
      <td>Torrance</td>
      <td>Philip Magruder Middle CSR rank: 8</td>
      <td>Philip Magruder Middle</td>
      <td>8</td>
    </tr>
    <tr>
      <th>960</th>
      <td>Torrance</td>
      <td>Riviera Elementary CSR rank: 10</td>
      <td>Riviera Elementary</td>
      <td>10</td>
    </tr>
    <tr>
      <th>961</th>
      <td>Torrance</td>
      <td>Seaside Elementary CSR rank: 10</td>
      <td>Seaside Elementary</td>
      <td>10</td>
    </tr>
    <tr>
      <th>962</th>
      <td>Torrance</td>
      <td>Kurt T. Shery High (Continuation) CSR rank: 3</td>
      <td>Kurt T. Shery High (Continuation)</td>
      <td>3</td>
    </tr>
    <tr>
      <th>963</th>
      <td>Torrance</td>
      <td>South High CSR rank: 10</td>
      <td>South High</td>
      <td>10</td>
    </tr>
    <tr>
      <th>964</th>
      <td>Torrance</td>
      <td>Torrance Elementary CSR rank: 5</td>
      <td>Torrance Elementary</td>
      <td>5</td>
    </tr>
    <tr>
      <th>965</th>
      <td>Torrance</td>
      <td>Torrance High CSR rank: 9</td>
      <td>Torrance High</td>
      <td>9</td>
    </tr>
    <tr>
      <th>966</th>
      <td>Torrance</td>
      <td>Towers Elementary CSR rank: 9</td>
      <td>Towers Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>967</th>
      <td>Torrance</td>
      <td>Victor Elementary CSR rank: 9</td>
      <td>Victor Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>968</th>
      <td>Torrance</td>
      <td>Walteria Elementary CSR rank: 9</td>
      <td>Walteria Elementary</td>
      <td>9</td>
    </tr>
    <tr>
      <th>969</th>
      <td>Torrance</td>
      <td>West High CSR rank: 10</td>
      <td>West High</td>
      <td>10</td>
    </tr>
    <tr>
      <th>970</th>
      <td>Torrance</td>
      <td>Yukon Elementary CSR rank: 6</td>
      <td>Yukon Elementary</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
<p>772 rows × 4 columns</p>
</div>




```python
#Group by City, aggregation average by Gini index

city_csr_df = school_csr_df.groupby(["CITY"])['CSR'].agg(['mean']).sort_index().reset_index()
city_csr_df= city_csr_df.rename(columns={"mean":"CSR_AVG"})

city_csr_df=city_csr_df.sort_values(by='CSR_AVG', ascending=True)
city_csr_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CITY</th>
      <th>CSR_AVG</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Inglewood</td>
      <td>3.419355</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Palmdale</td>
      <td>3.550000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Los Angeles</td>
      <td>4.316306</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Pasadena</td>
      <td>4.461538</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Long Beach</td>
      <td>5.563380</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Alhambra</td>
      <td>6.769231</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Glendale</td>
      <td>7.250000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Burbank</td>
      <td>7.388889</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Santa Clarita</td>
      <td>7.818182</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Torrance</td>
      <td>8.090909</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.set_style("whitegrid")
plt.figure(figsize=(15,7))
sns.barplot(x="CITY", y="CSR_AVG", data=city_csr_df, palette=sns.color_palette("RdYlGn", 10))

plt.xlabel("")
plt.ylabel("CSR AVG")
plt.title("School Ranking by Cities in LA County")

# Save the figure
plt.savefig("../Clean_Data/4.School_Ranking_by_City.png")
plt.show()
```


![png](Clean_Data/4.School_Ranking_by_City.png)



#### 5-1.get_zillow_data-Read before running the code

1. The Zillow API have 1000 daily request limitation, please use your own zws_id and gkey (google api) to run the code for your city (each person responsible for two city)
2. Various function were written to pull: 1) 200 lat/long by city per request; 2) Address generated by lat/long; 3) Zillow information based on address. Nothing need to change / update for the function when run through the code.
3. When first run the code, please go the the next Markdown to read the instruction. Before running the code to get housing data, please __enter the city you want to get the data with__.
4. To gather valid data, we removed data that could not generate complete and valid zillow housing information. In addition, we will remove any data that did not belong to the right city.
5. To insure that we have at least 50 valid data for each city, we run a loop at the end if valid data count is less than 50
6. Once we have more than 50 valid data for each city, the code will save the file into the Clean Data Folder
7. When code related to pull Lat/Lng information from Google API have "Index" error, that means we have reached the API limit and need to change the API key
8. When message code form zillow is 7, it means we have reached the API limit and we need to change to another key


```python
# ZILLOW DATA EXTRACTION WRITTEN BY SONIA YANG

# Dependencies
import requests
import urllib
import random
import math
import pandas as pd
import xml.etree.ElementTree as ET
import time
from config import zws_id, gkey # please use your own Zillow & Google API keys!

from urllib.request import urlopen
```


```python
# FUNCTION to grab the exact address based on longitude and latitude
# modified from here https://gist.github.com/bradmontgomery/5397472
# their example didn't include an API key, but I added it otherwise you'd hit the rate limit easily

def reverse_geocode(latitude, longitude):
    # Did the geocoding request comes from a device with a
    # location sensor? Must be either true or false
    sensor = 'true'

    # Hit Google's reverse geocoder directly
    # NOTE: I *think* their terms state that you're supposed to
    # use google maps if you use their api for anything.
    base = "https://maps.googleapis.com/maps/api/geocode/json?"
    params = "latlng={lat},{lon}&sensor={sen}&key={key}".format(
        lat=latitude,
        lon=longitude,
        sen=sensor,
        key=gkey
    )
    url = "{base}{params}".format(base=base, params=params)
    #print(url)
    response = requests.get(url).json()
    address = response['results'][0]['formatted_address']
    return address
```


```python
# FUNCTION to generate random lat & lng within a certain radius 
# modified from here: http://hadoopguru.blogspot.com/2014/12/python-generate-random-latitude-and.html
# changed to take in an empty initial dataframe and load in the data + return it
# this calls the reverse geocode function to grab the addresses of each randomly generated lat & lng

def generate_addresses(latitude, longitude, df):
    
    radius = 5000                         #Choose your own radius
    radiusInDegrees=radius/111300            
    r = radiusInDegrees

    counter = 0
    
    for i in range(1,50):                 #Choose number of Lat Long to be generated

        u = float(random.uniform(0.0,1.0))
        v = float(random.uniform(0.0,1.0))

        w = r * math.sqrt(u)
        t = 2 * math.pi * v
        x = w * math.cos(t) 
        y = w * math.sin(t)

        xLat  = x + latitude
        yLng = y + longitude

        df.set_value(counter, "latitude", xLat)
        df.set_value(counter, "longitude", yLng)
        
        #print(format(counter) + ": " + format(xLat) + ", " + format(yLng))
        address = reverse_geocode(xLat, yLng).split(',')
        citystatezip = address[1] + address[2]
        
        df.set_value(counter, "address", address[0])
        df.set_value(counter, "city_state_zip", citystatezip)
        
        # Add to counter
        counter = counter + 1
    
    return df
```


```python
# FUNCTION to call Zillow API's GetSearchResults and will check to see if a house exists at that address
# message code will be written to dataframe
# zillow url format
# http://www.zillow.com/webservice/GetSearchResults.htm?zws-id=<ZWSID>&address=2114+Bigelow+Ave&citystatezip=Seattle%2C+WA
        
def get_message_codes(df):

    for index, row in df.iterrows():

        try:
            url = 'https://www.zillow.com/webservice/GetSearchResults.htm?zws-id='
            address = row['address']
            citystatezip =row['city_state_zip']


            query_url = url + zws_id + '&address=' + urllib.parse.quote(address) + '&citystatezip=' + urllib.parse.quote(citystatezip) 
            #print(query_url)

            root = ET.parse(urlopen(query_url)).getroot()

            for message in root.iter('message'):
                message_code = message[1].text

            print(format(index) + ": " + message_code)

            df.set_value(index, 'message_code', message_code)

            time.sleep(0.5) #necessary bc bombarding Zillow with API calls doesn't allow enough time to respond to each

        except:
            break
    
```


```python
# FUNCTION to call Zillow's GetDeepSearchResults and look up Zestimate, bed, and bath
# http://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=<ZWSID>&address=2114+Bigelow+Ave&citystatezip=Seattle%2C+WA
# there are some limitations such as multiple zestimates depending on when the house was sold/if it was sold multiple times
# the code to handle that would get too convoluted so I am just writing in the most recent (according to the API) values
# probably not what we would do in real life
# but a decision we made re: the scope of a classroom project on a short time constraint

def search_zillow(df):
    
    for index, row in df.iterrows():
        try:
            url = 'https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id='
            address = df['address'][index]
            citystatezip = df['city_state_zip'][index]


            query_url = url + zws_id + '&address=' + urllib.parse.quote(address) + '&citystatezip=' + urllib.parse.quote(citystatezip) 


            root = ET.parse(urlopen(query_url)).getroot()

            print("row " + format(index) + ": " + address + citystatezip)
            print(query_url)

            '''
               "year built","lot size","finished sq ft"'''
            
            #zpid
            for zpid in root.iter('zpid'):
                df.set_value(index,'zpid', zpid.text)
            
            # we already have the address from the address + citystatezip variables
            # so we don't need to grab it again
            # same with lat & lng already being in the table
            
            #valuation (high and low)
            for valuation in root.iter('valuationRange'):
                highValuation = valuation[1].text
                lowValuation = valuation[0].text
                df.set_value(index, 'valuation_high', highValuation)
                df.set_value(index, 'valuation_low', lowValuation)
            
            #zestimate
            for zestimate in root.iter('zestimate'):
                zestimate_value = zestimate[0].text

                if zestimate_value is None:
                    print('not for sale')
                else:
                    print ('zestimate (value): ' + format(zestimate[0].text)) 
                    df.set_value(index, 'zestimate', zestimate_value)
             
            #home value index
            for zindexValue in root.iter('zindexValue'):
                df.set_value(index, 'home value index', zindexValue.text)
            
            #tax assessment
            for taxAssessment in root.iter('taxAssessment'):
                df.set_value(index, 'tax assessment', taxAssessment.text)
                
            #tax assessment year
            for taxAssessmentYear in root.iter('taxAssessmentYear'):
                df.set_value(index, 'tax assess year', taxAssessmentYear.text)
                
            #year built
            for yearBuilt in root.iter('yearBuilt'):
                df.set_value(index, 'year built', yearBuilt.text)
             
            #lot size sq ft
            for lotSizeSqFt in root.iter('lotSizeSqFt'):
                df.set_value(index, 'lot size', lotSizeSqFt.text)
            
            #finished sq ft
            for finishedSqFt in root.iter('finishedSqFt'):
                df.set_value(index, 'finished sq ft', finishedSqFt.text)
            
            #bedrooms
            for bedroom in root.iter('bedrooms'):
                bedrooms = bedroom.text
                #print("bedrooms: " + bedrooms)
                df.set_value(index, 'bedrooms', bedrooms)

            #bathrooms
            for bathroom in root.iter('bathrooms'):
                bathrooms = bathroom.text
                #print("bathrooms: " + bathrooms + "\n")
                df.set_value(index, 'bathrooms', bathrooms)           
            
            print('\n')

            time.sleep(0.5) 


        except:
            break

```

<h2>HOW TO RUN THIS CODE</h2>
<ol>
<li>Initialize an empty dataframe with the fields as marked below</li>
<li>Call the <strong>generate_addresses</strong> function passing in your empty dataframe</li>
<li>Call the <strong>get_message_codes</strong> to update your dataframe with message codes indicating whether or not a valid property exists at each address. <strong>IMPORTANT:</strong> please register your own Zillow account/get your own key for this!! If we all keep using the same one we'll easily hit the rate limit </li>
<li>Drop the rows in the dataframe for which a property does not exist at that address</li>
<li>Call the <strong>search_zillow</strong> function to get the zestimate (aka price of the property), # of bedrooms, and # of bathrooms</li>
<li>I did not include it in my code, but once you get a sample size of data that you are satisfied with for the city, maybe write it out to a CSV so you don't have to keep running this code/can use it later</li>
</ol>

feel free to comment out my print statements while the functions are running if you find them distracting


```python
# Read cities file to pull the Latitude and Longtitude
Cities=pd.read_csv('../Raw_Data/LA_cities_Lat_lng_codes_data.csv')
print(f'{Cities["address"]}')
city1 = input("Please input first city your want to pull data")
selectcity = Cities.loc[Cities["address"] == city1, :]
LAT = selectcity.iloc[0,1]
LNG = selectcity.iloc[0,2]
```

    0       Los Angeles
    1        Long Beach
    2          Glendale
    3         Lancaster
    4          Palmdale
    5     Santa Clarita
    6            Pomona
    7          Torrance
    8          Pasadena
    9         Inglewood
    10          Compton
    11           Downey
    12      West Covina
    13          Norwalk
    14          Burbank
    15       South Gate
    16         El Monte
    17         Whittier
    18         Alhambra
    Name: address, dtype: object
    Please input first city your want to pull dataTorrance
    


```python
# HOW TO RUN ALL THE FUNCTIONS, USING LOS ANGELES AS AN EXAMPLE

# coordinates taken from the CitiesGeo_Output.csv
# we should manually run the following code on each individual city instead of nesting it in another loop
# while this may be hardcoded, it's better than waiting on one gigantic loop that takes forever

# STEP 1: INITALIZE THE DATAFRAME
# if we need any more fields, let me know
la_df = pd.DataFrame({"zpid": '',
                      "address":'',
                      "city_state_zip":'',
                      "latitude":'',
                      "longitude":'',
                      "message_code":'',
                      "zestimate":'',
                      "valuation_high":'',
                      "valuation_low": '',
                      "home value index":'',
                      "tax assessment":'',
                      "tax assess year":'',
                      "year built":'',
                      "lot size":'',
                      "finished sq ft":'',
                      "bedrooms":'',
                      "bathrooms":''}, index=[0])

# reorder the columns
la_df = la_df[["zpid", "address","city_state_zip","latitude","longitude","message_code","zestimate",
               "valuation_high","valuation_low","home value index","tax assessment","tax assess year",
               "year built","lot size","finished sq ft","bedrooms","bathrooms"]]

# STEP 2: GENERATE RANDOM ADDRESSES IN THE DESIGNATED AREA
# pass in the coordinates for Los Angeles plus the empty dataframe
generate_addresses(LAT,LNG, la_df) 

#la_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td></td>
      <td>23536 Evalyn Ave</td>
      <td>Torrance CA 90505</td>
      <td>33.8117</td>
      <td>-118.359</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>3480 Del Amo Cir N</td>
      <td>Torrance CA 90503</td>
      <td>33.8338</td>
      <td>-118.346</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>841-899 Sartori Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8382</td>
      <td>-118.319</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>3110 Merrill Dr</td>
      <td>Torrance CA 90503</td>
      <td>33.8301</td>
      <td>-118.342</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>1536 W 222nd St</td>
      <td>Torrance CA 90501</td>
      <td>33.8255</td>
      <td>-118.305</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>3737 Pacific Coast Hwy</td>
      <td>Torrance CA 90505</td>
      <td>33.8051</td>
      <td>-118.35</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>4441 Redondo Beach Blvd</td>
      <td>Lawndale CA 90260</td>
      <td>33.8735</td>
      <td>-118.354</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>3703-3777 Redondo Beach Blvd</td>
      <td>Torrance CA 90504</td>
      <td>33.8802</td>
      <td>-118.34</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>1517-1521 Crenshaw Blvd</td>
      <td>Torrance CA 90501</td>
      <td>33.8332</td>
      <td>-118.329</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>1111 Barbara St</td>
      <td>Redondo Beach CA 90277</td>
      <td>33.831</td>
      <td>-118.375</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>2377 Del Amo Blvd</td>
      <td>Torrance CA 90501</td>
      <td>33.8473</td>
      <td>-118.326</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>NaN</td>
      <td>4600-4698 Vista Montana</td>
      <td>Torrance CA 90505</td>
      <td>33.8051</td>
      <td>-118.366</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>NaN</td>
      <td>2601-2899 W 177th St</td>
      <td>Torrance CA 90504</td>
      <td>33.8704</td>
      <td>-118.324</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>13</th>
      <td>NaN</td>
      <td>20318-20326 Madison St</td>
      <td>Torrance CA 90503</td>
      <td>33.8479</td>
      <td>-118.348</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>NaN</td>
      <td>2801 Sepulveda Blvd</td>
      <td>Torrance CA 90505</td>
      <td>33.8245</td>
      <td>-118.332</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>NaN</td>
      <td>3132 185th St</td>
      <td>Torrance CA 90504</td>
      <td>33.8626</td>
      <td>-118.328</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>16</th>
      <td>NaN</td>
      <td>19600 S Western Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.852</td>
      <td>-118.309</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17</th>
      <td>NaN</td>
      <td>2694-2714 Del Amo Blvd</td>
      <td>Torrance CA 90503</td>
      <td>33.8468</td>
      <td>-118.335</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18</th>
      <td>NaN</td>
      <td>2360 Plaza del Amo</td>
      <td>Torrance CA 90501</td>
      <td>33.8299</td>
      <td>-118.324</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19</th>
      <td>NaN</td>
      <td>2108 Ripley Ave</td>
      <td>Redondo Beach CA 90278</td>
      <td>33.861</td>
      <td>-118.373</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>20</th>
      <td>NaN</td>
      <td>4109 Emerald St</td>
      <td>Torrance CA 90503</td>
      <td>33.8421</td>
      <td>-118.357</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21</th>
      <td>NaN</td>
      <td>2127 W 237th St</td>
      <td>Torrance CA 90501</td>
      <td>33.81</td>
      <td>-118.318</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22</th>
      <td>NaN</td>
      <td>19205 Prairie Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.8561</td>
      <td>-118.346</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>23</th>
      <td>NaN</td>
      <td>19031-19079 S Western Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8577</td>
      <td>-118.31</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>24</th>
      <td>NaN</td>
      <td>4413-4417 W 234th St</td>
      <td>Torrance CA 90505</td>
      <td>33.8142</td>
      <td>-118.36</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25</th>
      <td>NaN</td>
      <td>19601-19771 Entradero Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.8518</td>
      <td>-118.369</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>26</th>
      <td>NaN</td>
      <td>3550w W Carson St</td>
      <td>Torrance CA 90503</td>
      <td>33.8306</td>
      <td>-118.351</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>27</th>
      <td>NaN</td>
      <td>21734 Evalyn Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.8307</td>
      <td>-118.362</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>28</th>
      <td>NaN</td>
      <td>3000-3146 Rolling Hills Rd</td>
      <td>Torrance CA 90505</td>
      <td>33.7927</td>
      <td>-118.344</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>29</th>
      <td>NaN</td>
      <td>4202 Carmen St</td>
      <td>Torrance CA 90503</td>
      <td>33.833</td>
      <td>-118.358</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>30</th>
      <td>NaN</td>
      <td>5528-5530 Towers St</td>
      <td>Torrance CA 90503</td>
      <td>33.8548</td>
      <td>-118.374</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>31</th>
      <td>NaN</td>
      <td>18727 Prairie Ave</td>
      <td>Torrance CA 90504</td>
      <td>33.861</td>
      <td>-118.344</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>32</th>
      <td>NaN</td>
      <td>18700 Crenshaw Blvd</td>
      <td>Torrance CA 90504</td>
      <td>33.8613</td>
      <td>-118.325</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>33</th>
      <td>NaN</td>
      <td>224N N Prospect Ave</td>
      <td>Redondo Beach CA 90277</td>
      <td>33.8455</td>
      <td>-118.377</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>34</th>
      <td>NaN</td>
      <td>2641-2677 Del Amo Blvd</td>
      <td>Torrance CA 90503</td>
      <td>33.8499</td>
      <td>-118.334</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>35</th>
      <td>NaN</td>
      <td>Del Amo Cir W</td>
      <td>Torrance CA 90503</td>
      <td>33.83</td>
      <td>-118.354</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>36</th>
      <td>NaN</td>
      <td>4230-4592 Vista Montana</td>
      <td>Torrance CA 90505</td>
      <td>33.8052</td>
      <td>-118.361</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>37</th>
      <td>NaN</td>
      <td>4064-4068 Vía Valmonte</td>
      <td>Palos Verdes Estates CA 90274</td>
      <td>33.7976</td>
      <td>-118.361</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>38</th>
      <td>NaN</td>
      <td>18310-18316 Glenburn Ave</td>
      <td>Torrance CA 90504</td>
      <td>33.8644</td>
      <td>-118.331</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>39</th>
      <td>NaN</td>
      <td>1500-1524 Border Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8338</td>
      <td>-118.313</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>40</th>
      <td>NaN</td>
      <td>3230-3300 Fujita St</td>
      <td>Torrance CA 90505</td>
      <td>33.8147</td>
      <td>-118.343</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>41</th>
      <td>NaN</td>
      <td>22733 Anza Ave</td>
      <td>Torrance CA 90505</td>
      <td>33.8216</td>
      <td>-118.36</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>42</th>
      <td>NaN</td>
      <td>3116-3176 Skypark Dr</td>
      <td>Torrance CA 90505</td>
      <td>33.8064</td>
      <td>-118.344</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>43</th>
      <td>NaN</td>
      <td>19324-19328 Donora Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.8547</td>
      <td>-118.367</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>44</th>
      <td>NaN</td>
      <td>Dominguez St</td>
      <td>Torrance CA 90501</td>
      <td>33.8409</td>
      <td>-118.329</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>45</th>
      <td>NaN</td>
      <td>20019-20227 Van Ness Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8527</td>
      <td>-118.323</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>46</th>
      <td>NaN</td>
      <td>2602 Cabrillo Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8214</td>
      <td>-118.315</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>47</th>
      <td>NaN</td>
      <td>2728 Arlington Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8208</td>
      <td>-118.319</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>48</th>
      <td>NaN</td>
      <td>1101-1209 W 220th St</td>
      <td>Torrance CA 90502</td>
      <td>33.8281</td>
      <td>-118.297</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# STEP 3: CALL THE ZILLOW API TO GET MESSAGE CODES
# 0 means there is a valid property at that address
# 508 and anything else means there isn't
# if you get nothing but invalid message codes, re-run STEP 2
# you might have to sign up for a new Zillow account if you keep getting invalid results here
# there is a possibility you hit the rate limit

get_message_codes(la_df)
```

    0: 0
    1: 508
    2: 508
    3: 0
    4: 0
    5: 508
    6: 508
    7: 508
    8: 508
    9: 0
    10: 0
    11: 508
    12: 508
    13: 508
    14: 0
    15: 0
    16: 508
    17: 508
    18: 508
    19: 0
    20: 0
    21: 0
    22: 508
    23: 508
    24: 508
    25: 508
    26: 508
    27: 0
    28: 508
    29: 0
    30: 508
    31: 0
    32: 0
    33: 0
    34: 508
    35: 508
    36: 508
    37: 508
    38: 508
    39: 508
    40: 508
    41: 0
    42: 508
    43: 508
    44: 508
    45: 508
    46: 0
    47: 0
    48: 508
    


```python
# STEP 4: DROP INVALID ENTRIES FROM DATAFRAME 
# cull all the rows where houses do not exist at the address
# take what is valid (message code of '0')
# the code sometimes might break/not get a response from the server so it's better to take what IS valid

la_df = la_df[la_df.message_code == '0']

# take out items that does not belong to the select city
la_df=la_df[la_df.city_state_zip.str.contains(city1) == True]

la_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td></td>
      <td>23536 Evalyn Ave</td>
      <td>Torrance CA 90505</td>
      <td>33.8117</td>
      <td>-118.359</td>
      <td>0</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>3110 Merrill Dr</td>
      <td>Torrance CA 90503</td>
      <td>33.8301</td>
      <td>-118.342</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>1536 W 222nd St</td>
      <td>Torrance CA 90501</td>
      <td>33.8255</td>
      <td>-118.305</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>2377 Del Amo Blvd</td>
      <td>Torrance CA 90501</td>
      <td>33.8473</td>
      <td>-118.326</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>NaN</td>
      <td>2801 Sepulveda Blvd</td>
      <td>Torrance CA 90505</td>
      <td>33.8245</td>
      <td>-118.332</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>NaN</td>
      <td>3132 185th St</td>
      <td>Torrance CA 90504</td>
      <td>33.8626</td>
      <td>-118.328</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>20</th>
      <td>NaN</td>
      <td>4109 Emerald St</td>
      <td>Torrance CA 90503</td>
      <td>33.8421</td>
      <td>-118.357</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21</th>
      <td>NaN</td>
      <td>2127 W 237th St</td>
      <td>Torrance CA 90501</td>
      <td>33.81</td>
      <td>-118.318</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>27</th>
      <td>NaN</td>
      <td>21734 Evalyn Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.8307</td>
      <td>-118.362</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>29</th>
      <td>NaN</td>
      <td>4202 Carmen St</td>
      <td>Torrance CA 90503</td>
      <td>33.833</td>
      <td>-118.358</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>31</th>
      <td>NaN</td>
      <td>18727 Prairie Ave</td>
      <td>Torrance CA 90504</td>
      <td>33.861</td>
      <td>-118.344</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>32</th>
      <td>NaN</td>
      <td>18700 Crenshaw Blvd</td>
      <td>Torrance CA 90504</td>
      <td>33.8613</td>
      <td>-118.325</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>41</th>
      <td>NaN</td>
      <td>22733 Anza Ave</td>
      <td>Torrance CA 90505</td>
      <td>33.8216</td>
      <td>-118.36</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>46</th>
      <td>NaN</td>
      <td>2602 Cabrillo Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8214</td>
      <td>-118.315</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>47</th>
      <td>NaN</td>
      <td>2728 Arlington Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8208</td>
      <td>-118.319</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# STEP 5: SEARCH ZILLOW AND GET ZESTIMATE, BEDROOMS, & BATHROOMS
# fill the dataframe with the data

search_zillow(la_df)
la_df
```

    row 0: 23536 Evalyn Ave Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=23536%20Evalyn%20Ave&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 942689
    
    
    row 3: 3110 Merrill Dr Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=3110%20Merrill%20Dr&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 457235
    zestimate (value): 632955
    zestimate (value): 574763
    zestimate (value): 456297
    zestimate (value): 618609
    zestimate (value): 618609
    zestimate (value): 565105
    zestimate (value): 779474
    zestimate (value): 570333
    zestimate (value): 533059
    zestimate (value): 439905
    zestimate (value): 798844
    zestimate (value): 709909
    zestimate (value): 709529
    zestimate (value): 572799
    zestimate (value): 582634
    zestimate (value): 892815
    zestimate (value): 718690
    zestimate (value): 450666
    zestimate (value): 885144
    zestimate (value): 739529
    zestimate (value): 481015
    zestimate (value): 382886
    zestimate (value): 721446
    
    
    row 4: 1536 W 222nd St Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=1536%20W%20222nd%20St&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 598835
    
    
    row 10: 2377 Del Amo Blvd Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2377%20Del%20Amo%20Blvd&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 645824
    
    
    row 14: 2801 Sepulveda Blvd Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2801%20Sepulveda%20Blvd&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 822600
    zestimate (value): 806887
    zestimate (value): 822812
    zestimate (value): 810042
    zestimate (value): 799809
    zestimate (value): 798398
    zestimate (value): 798307
    zestimate (value): 803576
    zestimate (value): 798298
    zestimate (value): 798638
    zestimate (value): 834978
    zestimate (value): 803835
    zestimate (value): 808585
    zestimate (value): 801419
    zestimate (value): 883463
    zestimate (value): 806779
    zestimate (value): 809915
    zestimate (value): 820917
    zestimate (value): 799065
    zestimate (value): 802178
    zestimate (value): 820822
    zestimate (value): 799600
    zestimate (value): 832156
    zestimate (value): 798980
    zestimate (value): 801896
    
    
    row 15: 3132 185th St Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=3132%20185th%20St&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 721006
    
    
    row 20: 4109 Emerald St Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=4109%20Emerald%20St&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 1451973
    
    
    row 21: 2127 W 237th St Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2127%20W%20237th%20St&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 875936
    
    
    row 27: 21734 Evalyn Ave Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=21734%20Evalyn%20Ave&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 957442
    
    
    row 29: 4202 Carmen St Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=4202%20Carmen%20St&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 930185
    
    
    row 31: 18727 Prairie Ave Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=18727%20Prairie%20Ave&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 968178
    
    
    row 32: 18700 Crenshaw Blvd Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=18700%20Crenshaw%20Blvd&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 604186
    
    
    row 41: 22733 Anza Ave Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=22733%20Anza%20Ave&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 859126
    
    
    row 46: 2602 Cabrillo Ave Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2602%20Cabrillo%20Ave&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 761337
    zestimate (value): 753742
    
    
    row 47: 2728 Arlington Ave Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2728%20Arlington%20Ave&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 617270
    
    
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21334983</td>
      <td>23536 Evalyn Ave</td>
      <td>Torrance CA 90505</td>
      <td>33.8117</td>
      <td>-118.359</td>
      <td>0</td>
      <td>942689</td>
      <td>989823</td>
      <td>895555</td>
      <td>855,300</td>
      <td>156339.0</td>
      <td>2017</td>
      <td>1962</td>
      <td>6213</td>
      <td>1764</td>
      <td>3</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2145608762</td>
      <td>3110 Merrill Dr</td>
      <td>Torrance CA 90503</td>
      <td>33.8301</td>
      <td>-118.342</td>
      <td>0</td>
      <td>721446</td>
      <td>815234</td>
      <td>483369</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1963</td>
      <td>174240</td>
      <td>1315</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>21265915</td>
      <td>1536 W 222nd St</td>
      <td>Torrance CA 90501</td>
      <td>33.8255</td>
      <td>-118.305</td>
      <td>0</td>
      <td>598835</td>
      <td>628777</td>
      <td>568893</td>
      <td>459,700</td>
      <td>334276.0</td>
      <td>2017</td>
      <td>1952</td>
      <td>7200</td>
      <td>1549</td>
      <td>3</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>21268886</td>
      <td>2377 Del Amo Blvd</td>
      <td>Torrance CA 90501</td>
      <td>33.8473</td>
      <td>-118.326</td>
      <td>0</td>
      <td>645824</td>
      <td>678115</td>
      <td>613533</td>
      <td>NaN</td>
      <td>449747.0</td>
      <td>2017</td>
      <td>1949</td>
      <td>4981</td>
      <td>1016</td>
      <td>3</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>21273938</td>
      <td>2801 Sepulveda Blvd</td>
      <td>Torrance CA 90505</td>
      <td>33.8245</td>
      <td>-118.332</td>
      <td>0</td>
      <td>801896</td>
      <td>841991</td>
      <td>761801</td>
      <td>NaN</td>
      <td>595241.0</td>
      <td>2017</td>
      <td>1995</td>
      <td>164221</td>
      <td>1809</td>
      <td>3</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>20372467</td>
      <td>3132 185th St</td>
      <td>Torrance CA 90504</td>
      <td>33.8626</td>
      <td>-118.328</td>
      <td>0</td>
      <td>721006</td>
      <td>757056</td>
      <td>684956</td>
      <td>630,700</td>
      <td>320768.0</td>
      <td>2017</td>
      <td>1950</td>
      <td>6499</td>
      <td>1256</td>
      <td>3</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>21332589</td>
      <td>4109 Emerald St</td>
      <td>Torrance CA 90503</td>
      <td>33.8421</td>
      <td>-118.357</td>
      <td>0</td>
      <td>1451973</td>
      <td>1655249</td>
      <td>1176098</td>
      <td>744,600</td>
      <td>541658.0</td>
      <td>2017</td>
      <td>1963</td>
      <td>6901</td>
      <td>4302</td>
      <td>8</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21279166</td>
      <td>2127 W 237th St</td>
      <td>Torrance CA 90501</td>
      <td>33.81</td>
      <td>-118.318</td>
      <td>0</td>
      <td>875936</td>
      <td>919733</td>
      <td>832139</td>
      <td>741,900</td>
      <td>105357.0</td>
      <td>2017</td>
      <td>1965</td>
      <td>5784</td>
      <td>2154</td>
      <td>5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>21328017</td>
      <td>21734 Evalyn Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.8307</td>
      <td>-118.362</td>
      <td>0</td>
      <td>957442</td>
      <td>1005314</td>
      <td>909570</td>
      <td>809,400</td>
      <td>934000.0</td>
      <td>2017</td>
      <td>1955</td>
      <td>6227</td>
      <td>1740</td>
      <td>4</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>21333339</td>
      <td>4202 Carmen St</td>
      <td>Torrance CA 90503</td>
      <td>33.833</td>
      <td>-118.358</td>
      <td>0</td>
      <td>930185</td>
      <td>976694</td>
      <td>883676</td>
      <td>809,400</td>
      <td>439353.0</td>
      <td>2017</td>
      <td>1956</td>
      <td>5601</td>
      <td>1720</td>
      <td>3</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>31</th>
      <td>20369833</td>
      <td>18727 Prairie Ave</td>
      <td>Torrance CA 90504</td>
      <td>33.861</td>
      <td>-118.344</td>
      <td>0</td>
      <td>968178</td>
      <td>1016587</td>
      <td>919769</td>
      <td>630,700</td>
      <td>691687.0</td>
      <td>2017</td>
      <td>NaN</td>
      <td>355408</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>32</th>
      <td>20372624</td>
      <td>18700 Crenshaw Blvd</td>
      <td>Torrance CA 90504</td>
      <td>33.8613</td>
      <td>-118.325</td>
      <td>0</td>
      <td>604186</td>
      <td>634395</td>
      <td>573977</td>
      <td>630,700</td>
      <td>386720.0</td>
      <td>2017</td>
      <td>1951</td>
      <td>5644</td>
      <td>850</td>
      <td>3</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>41</th>
      <td>21333846</td>
      <td>22733 Anza Ave</td>
      <td>Torrance CA 90505</td>
      <td>33.8216</td>
      <td>-118.36</td>
      <td>0</td>
      <td>859126</td>
      <td>902082</td>
      <td>816170</td>
      <td>869,800</td>
      <td>643589.0</td>
      <td>2017</td>
      <td>1953</td>
      <td>5375</td>
      <td>1616</td>
      <td>3</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>46</th>
      <td>2117437376</td>
      <td>2602 Cabrillo Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8214</td>
      <td>-118.315</td>
      <td>0</td>
      <td>753742</td>
      <td>829116</td>
      <td>693443</td>
      <td>595,500</td>
      <td>461549.0</td>
      <td>2017</td>
      <td>1990</td>
      <td>5505</td>
      <td>1952</td>
      <td>4</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>47</th>
      <td>2101776885</td>
      <td>2728 Arlington Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8208</td>
      <td>-118.319</td>
      <td>0</td>
      <td>617270</td>
      <td>753069</td>
      <td>450607</td>
      <td>595,500</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# do any further data cleaning you need to yourself
# for example, dropping any rows with NaN values
la_df = la_df.dropna(axis=0, how='any')
la_df

# maybe write to CSV to store the data for usage later/before doing plots? so you don't have to rerun everything
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21334983</td>
      <td>23536 Evalyn Ave</td>
      <td>Torrance CA 90505</td>
      <td>33.8117</td>
      <td>-118.359</td>
      <td>0</td>
      <td>942689</td>
      <td>989823</td>
      <td>895555</td>
      <td>855,300</td>
      <td>156339.0</td>
      <td>2017</td>
      <td>1962</td>
      <td>6213</td>
      <td>1764</td>
      <td>3</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>21265915</td>
      <td>1536 W 222nd St</td>
      <td>Torrance CA 90501</td>
      <td>33.8255</td>
      <td>-118.305</td>
      <td>0</td>
      <td>598835</td>
      <td>628777</td>
      <td>568893</td>
      <td>459,700</td>
      <td>334276.0</td>
      <td>2017</td>
      <td>1952</td>
      <td>7200</td>
      <td>1549</td>
      <td>3</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>20372467</td>
      <td>3132 185th St</td>
      <td>Torrance CA 90504</td>
      <td>33.8626</td>
      <td>-118.328</td>
      <td>0</td>
      <td>721006</td>
      <td>757056</td>
      <td>684956</td>
      <td>630,700</td>
      <td>320768.0</td>
      <td>2017</td>
      <td>1950</td>
      <td>6499</td>
      <td>1256</td>
      <td>3</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>21332589</td>
      <td>4109 Emerald St</td>
      <td>Torrance CA 90503</td>
      <td>33.8421</td>
      <td>-118.357</td>
      <td>0</td>
      <td>1451973</td>
      <td>1655249</td>
      <td>1176098</td>
      <td>744,600</td>
      <td>541658.0</td>
      <td>2017</td>
      <td>1963</td>
      <td>6901</td>
      <td>4302</td>
      <td>8</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21279166</td>
      <td>2127 W 237th St</td>
      <td>Torrance CA 90501</td>
      <td>33.81</td>
      <td>-118.318</td>
      <td>0</td>
      <td>875936</td>
      <td>919733</td>
      <td>832139</td>
      <td>741,900</td>
      <td>105357.0</td>
      <td>2017</td>
      <td>1965</td>
      <td>5784</td>
      <td>2154</td>
      <td>5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>21328017</td>
      <td>21734 Evalyn Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.8307</td>
      <td>-118.362</td>
      <td>0</td>
      <td>957442</td>
      <td>1005314</td>
      <td>909570</td>
      <td>809,400</td>
      <td>934000.0</td>
      <td>2017</td>
      <td>1955</td>
      <td>6227</td>
      <td>1740</td>
      <td>4</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>21333339</td>
      <td>4202 Carmen St</td>
      <td>Torrance CA 90503</td>
      <td>33.833</td>
      <td>-118.358</td>
      <td>0</td>
      <td>930185</td>
      <td>976694</td>
      <td>883676</td>
      <td>809,400</td>
      <td>439353.0</td>
      <td>2017</td>
      <td>1956</td>
      <td>5601</td>
      <td>1720</td>
      <td>3</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>32</th>
      <td>20372624</td>
      <td>18700 Crenshaw Blvd</td>
      <td>Torrance CA 90504</td>
      <td>33.8613</td>
      <td>-118.325</td>
      <td>0</td>
      <td>604186</td>
      <td>634395</td>
      <td>573977</td>
      <td>630,700</td>
      <td>386720.0</td>
      <td>2017</td>
      <td>1951</td>
      <td>5644</td>
      <td>850</td>
      <td>3</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>41</th>
      <td>21333846</td>
      <td>22733 Anza Ave</td>
      <td>Torrance CA 90505</td>
      <td>33.8216</td>
      <td>-118.36</td>
      <td>0</td>
      <td>859126</td>
      <td>902082</td>
      <td>816170</td>
      <td>869,800</td>
      <td>643589.0</td>
      <td>2017</td>
      <td>1953</td>
      <td>5375</td>
      <td>1616</td>
      <td>3</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>46</th>
      <td>2117437376</td>
      <td>2602 Cabrillo Ave</td>
      <td>Torrance CA 90501</td>
      <td>33.8214</td>
      <td>-118.315</td>
      <td>0</td>
      <td>753742</td>
      <td>829116</td>
      <td>693443</td>
      <td>595,500</td>
      <td>461549.0</td>
      <td>2017</td>
      <td>1990</td>
      <td>5505</td>
      <td>1952</td>
      <td>4</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# review current data and see if more data is needed (at least 50 valid data per city)
add_df = pd.DataFrame(la_df)
final_df = add_df
final_df = final_df.reset_index(drop=True)
len(final_df)
```




    10




```python
# If minimum 50 valid data counts is not met, we will loop through the codes above to make sure we have sufficient data
while(len(final_df)<50):
    generate_addresses(LAT,LNG, la_df) 
    get_message_codes(la_df)
    la_df = la_df[la_df.message_code == '0']
    la_df=la_df[la_df.city_state_zip.str.contains(city1) == True]
    search_zillow(la_df)
    la_df = la_df.dropna(axis=0, how='any')
    add_df = add_df.append(la_df, ignore_index=True)
    final_df = add_df.drop_duplicates()
len(final_df)
```

    C:\Users\liang\Anaconda3\envs\pydata\lib\site-packages\pandas\core\frame.py:1861: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      self.loc[index, col] = value
    

    0: 508
    4: 508
    15: 508
    20: 508
    21: 508
    27: 508
    29: 508
    32: 0
    41: 0
    46: 0
    1: 0
    2: 0
    3: 508
    5: 0
    6: 508
    7: 0
    8: 508
    9: 0
    10: 0
    11: 508
    12: 508
    13: 508
    14: 508
    16: 0
    17: 508
    18: 508
    19: 508
    22: 0
    23: 0
    24: 508
    25: 508
    26: 508
    28: 508
    30: 508
    31: 508
    33: 508
    34: 508
    35: 508
    36: 508
    37: 0
    38: 0
    39: 508
    40: 508
    42: 508
    43: 508
    44: 508
    45: 0
    47: 508
    48: 508
    row 32: 1924 Middlebrook Rd Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=1924%20Middlebrook%20Rd&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 899318
    
    
    row 41: 22741 Date Ave Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=22741%20Date%20Ave&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 805505
    
    
    row 46: 19802 Tomlee Ave Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=19802%20Tomlee%20Ave&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 1022016
    
    
    row 1: 2707 W 179th St Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2707%20W%20179th%20St&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 717283
    
    
    row 5: 17119 Faysmith Ave Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=17119%20Faysmith%20Ave&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 768533
    
    
    row 7: 5405 Towers St Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=5405%20Towers%20St&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 1029656
    
    
    row 10: 23003 Doris Way Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=23003%20Doris%20Way&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 1321069
    
    
    row 22: 2533 Dorset Dr Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2533%20Dorset%20Dr&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 950434
    
    
    row 38: 2306 Cabrillo Ave Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2306%20Cabrillo%20Ave&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 613516
    
    
    row 45: 1302 W 223rd St Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=1302%20W%20223rd%20St&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 672245
    
    
    32: 0
    41: 0
    46: 508
    1: 508
    5: 508
    7: 508
    10: 508
    45: 508
    0: 0
    2: 508
    3: 0
    4: 508
    6: 508
    8: 508
    9: 508
    11: 508
    12: 0
    13: 508
    14: 508
    15: 508
    16: 0
    17: 508
    18: 508
    19: 508
    20: 508
    21: 0
    22: 508
    23: 0
    24: 508
    25: 508
    26: 0
    27: 508
    28: 0
    29: 0
    30: 508
    31: 508
    33: 0
    34: 508
    35: 508
    36: 0
    37: 508
    38: 508
    39: 0
    40: 0
    42: 508
    43: 508
    44: 0
    47: 508
    48: 508
    row 41: 24245 Ward St Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=24245%20Ward%20St&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 972609
    
    
    row 0: 5321 Jacques St Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=5321%20Jacques%20St&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 1240347
    
    
    row 16: 1625 Maple Ave Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=1625%20Maple%20Ave&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 873059
    
    
    row 23: 1445 W 224th St Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=1445%20W%20224th%20St&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 466603
    
    
    row 28: 2460 229th Pl Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2460%20229th%20Pl&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 867677
    
    
    row 29: 3462 W 170th St Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=3462%20W%20170th%20St&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 658930
    
    
    row 33: 4033 184th St Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=4033%20184th%20St&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 762793
    
    
    row 36: 2559 W 235th St Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2559%20W%20235th%20St&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 626450
    
    
    row 39: 21122 Harvard Blvd Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=21122%20Harvard%20Blvd&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 559206
    
    
    row 40: 2920 W 235th St Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2920%20W%20235th%20St&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 784200
    zestimate (value): 607613
    
    
    41: 508
    0: 508
    16: 508
    28: 508
    29: 508
    33: 508
    39: 508
    1: 0
    2: 508
    3: 508
    4: 508
    5: 508
    6: 508
    7: 508
    8: 508
    9: 0
    10: 0
    11: 508
    12: 508
    13: 508
    14: 508
    15: 508
    17: 508
    18: 508
    19: 0
    20: 508
    21: 508
    22: 508
    23: 508
    24: 508
    25: 508
    26: 508
    27: 508
    30: 0
    31: 508
    32: 508
    34: 0
    35: 508
    36: 0
    37: 508
    38: 508
    40: 0
    42: 508
    43: 508
    44: 0
    45: 508
    46: 0
    47: 0
    48: 508
    row 1: 17801 Glenburn Ave Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=17801%20Glenburn%20Ave&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 710238
    
    
    row 10: 19417 Anza Ave Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=19417%20Anza%20Ave&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 797979
    
    
    row 30: 1551 W 206th St Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=1551%20W%20206th%20St&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 562395
    
    
    row 34: 5028 Lee St Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=5028%20Lee%20St&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 1016519
    
    
    row 36: 20357 Madison St Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=20357%20Madison%20St&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 905076
    
    
    row 46: 21146 Harvard Blvd Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=21146%20Harvard%20Blvd&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 674316
    
    
    row 47: 1349 W 221st St Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=1349%20W%20221st%20St&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 515391
    
    
    1: 0
    10: 508
    30: 0
    34: 0
    36: 508
    46: 508
    47: 0
    0: 508
    2: 508
    3: 508
    4: 508
    5: 508
    6: 0
    7: 508
    8: 0
    9: 0
    11: 508
    12: 508
    13: 508
    14: 508
    15: 508
    16: 0
    17: 508
    18: 508
    19: 508
    20: 508
    21: 508
    22: 508
    23: 508
    24: 0
    25: 508
    26: 0
    27: 508
    28: 0
    29: 0
    31: 508
    32: 508
    33: 508
    35: 508
    37: 508
    38: 508
    39: 0
    40: 508
    41: 508
    42: 508
    43: 508
    44: 508
    45: 508
    48: 508
    row 1: 5013 Deelane St Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=5013%20Deelane%20St&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 956409
    
    
    row 30: 3399 Candlewood Rd Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=3399%20Candlewood%20Rd&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 1021805
    
    
    row 34: 18114 Manhattan Pl Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=18114%20Manhattan%20Pl&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 656241
    
    
    row 6: 17318 Casimir Ave Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=17318%20Casimir%20Ave&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 528203
    
    
    row 8: 2365 Plaza del Amo Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2365%20Plaza%20del%20Amo&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 501828
    
    
    row 9: 1435 W 218th St Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=1435%20W%20218th%20St&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 669819
    
    
    row 24: 1648 W 227th St Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=1648%20W%20227th%20St&citystatezip=%20Torrance%20CA%2090501
    not for sale
    zestimate (value): 589690
    not for sale
    
    
    row 26: 21730 Ladeene Ave Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=21730%20Ladeene%20Ave&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 874133
    
    
    row 29: 3853 W 231st Pl Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=3853%20W%20231st%20Pl&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 1039879
    
    
    1: 0
    30: 508
    34: 508
    6: 508
    8: 508
    26: 508
    29: 508
    0: 508
    2: 508
    3: 508
    4: 508
    5: 508
    7: 0
    9: 508
    10: 0
    11: 508
    12: 508
    13: 508
    14: 0
    15: 508
    16: 0
    17: 0
    18: 0
    19: 0
    20: 508
    21: 0
    22: 508
    23: 508
    24: 508
    25: 508
    27: 0
    28: 0
    31: 508
    32: 508
    33: 508
    35: 508
    36: 0
    37: 508
    38: 508
    39: 508
    40: 508
    41: 508
    42: 508
    43: 0
    44: 508
    45: 0
    46: 0
    47: 508
    48: 508
    row 1: 3037 Lazy Meadow Dr Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=3037%20Lazy%20Meadow%20Dr&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 1096004
    
    
    row 10: 5457-5465 Sharynne Ln Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=5457-5465%20Sharynne%20Ln&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 1712821
    
    
    row 14: 18712 Felbar Ave Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=18712%20Felbar%20Ave&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 760967
    
    
    row 16: 4298 Michelle Dr Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=4298%20Michelle%20Dr&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 1121540
    
    
    row 17: 21020 Ladeene Ave Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=21020%20Ladeene%20Ave&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 1572946
    
    
    row 18: 3953 188th St Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=3953%20188th%20St&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 836513
    
    
    row 19: 4299 W 190th St Torrance CA 90504
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=4299%20W%20190th%20St&citystatezip=%20Torrance%20CA%2090504
    zestimate (value): 926908
    
    
    row 21: 4729 Deelane St Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=4729%20Deelane%20St&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 932905
    
    
    row 28: 2130 Plaza del Amo Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2130%20Plaza%20del%20Amo&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 613435
    zestimate (value): 613949
    zestimate (value): 615623
    zestimate (value): 613435
    zestimate (value): 624927
    zestimate (value): 581986
    zestimate (value): 622800
    zestimate (value): 617452
    zestimate (value): 620088
    zestimate (value): 621301
    zestimate (value): 623275
    zestimate (value): 616279
    zestimate (value): 615091
    zestimate (value): 616604
    zestimate (value): 612411
    zestimate (value): 617297
    zestimate (value): 607975
    zestimate (value): 561489
    zestimate (value): 621171
    zestimate (value): 621000
    zestimate (value): 627270
    zestimate (value): 623949
    zestimate (value): 614828
    zestimate (value): 582060
    zestimate (value): 610931
    
    
    row 36: 2445 W 232nd St Torrance CA 90501
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=2445%20W%20232nd%20St&citystatezip=%20Torrance%20CA%2090501
    zestimate (value): 1278215
    
    
    row 43: 3706 W 224th St Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=3706%20W%20224th%20St&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 811534
    
    
    row 45: 4730 Newton St Torrance CA 90505
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=4730%20Newton%20St&citystatezip=%20Torrance%20CA%2090505
    zestimate (value): 1159646
    
    
    row 46: 21832 Barbara St Torrance CA 90503
    https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id=X1-ZWz18olpf98c97_2xcn2&address=21832%20Barbara%20St&citystatezip=%20Torrance%20CA%2090503
    zestimate (value): 1263331
    
    
    




    52




```python
# review final city data before save the file
final_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>21334983</td>
      <td>1101-1105 Lilienthal Ln</td>
      <td>Redondo Beach CA 90278</td>
      <td>33.8642</td>
      <td>-118.366</td>
      <td>0</td>
      <td>942689</td>
      <td>989823</td>
      <td>895555</td>
      <td>855,300</td>
      <td>156339.0</td>
      <td>2017</td>
      <td>1962</td>
      <td>6213</td>
      <td>1764</td>
      <td>3</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21265915</td>
      <td>1536 W 222nd St</td>
      <td>Torrance CA 90501</td>
      <td>33.8255</td>
      <td>-118.305</td>
      <td>0</td>
      <td>598835</td>
      <td>628777</td>
      <td>568893</td>
      <td>459,700</td>
      <td>334276.0</td>
      <td>2017</td>
      <td>1952</td>
      <td>7200</td>
      <td>1549</td>
      <td>3</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20372467</td>
      <td>3132 185th St</td>
      <td>Torrance CA 90504</td>
      <td>33.8626</td>
      <td>-118.328</td>
      <td>0</td>
      <td>721006</td>
      <td>757056</td>
      <td>684956</td>
      <td>630,700</td>
      <td>320768.0</td>
      <td>2017</td>
      <td>1950</td>
      <td>6499</td>
      <td>1256</td>
      <td>3</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21332589</td>
      <td>4109 Emerald St</td>
      <td>Torrance CA 90503</td>
      <td>33.8421</td>
      <td>-118.357</td>
      <td>0</td>
      <td>1451973</td>
      <td>1655249</td>
      <td>1176098</td>
      <td>744,600</td>
      <td>541658.0</td>
      <td>2017</td>
      <td>1963</td>
      <td>6901</td>
      <td>4302</td>
      <td>8</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>21279166</td>
      <td>2127 W 237th St</td>
      <td>Torrance CA 90501</td>
      <td>33.81</td>
      <td>-118.318</td>
      <td>0</td>
      <td>875936</td>
      <td>919733</td>
      <td>832139</td>
      <td>741,900</td>
      <td>105357.0</td>
      <td>2017</td>
      <td>1965</td>
      <td>5784</td>
      <td>2154</td>
      <td>5</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Save file into Clean Data folder
final_df.to_csv(f'../Clean_Data/5-1.{city1}_zillow_data.csv')
```

#### 5-2.Combine Zillow Data


# Combine Zillow Data

1. The code is to combine all the Zillow data by cities into one big data frame
2. We also pull additional data from Zillow (rent / value change)


```python
# ZILLOW DATA Combined
# Dependencies
import numpy as np
import math
import pandas as pd
import time
import requests
import urllib
import random
import xml.etree.ElementTree as ET
from config import zws_id # please use your own Zillow API keys!
from urllib.request import urlopen
```


```python
# Read all zillow files by cities
Burbank_df=pd.read_csv('../Clean_Data/5-1.Burbank_zillow_data.csv')
Glendale_df=pd.read_csv('../Clean_Data/5-1.Glendale_zillow_data.csv')
Inglewood_df=pd.read_csv('../Clean_Data/5-1.Inglewood_zillow_data.csv')
Alhambra_df=pd.read_csv('../Clean_Data/5-1.Alhambra_zillow_data.csv')
Longbeach_df=pd.read_csv('../Clean_Data/5-1.Long Beach_zillow_data.csv')
Losangeles_df=pd.read_csv('../Clean_Data/5-1.Los Angeles_zillow_data.csv')
Palmdale_df=pd.read_csv('../Clean_Data/5-1.Palmdale_zillow_data.csv')
Pasadena_df=pd.read_csv('../Clean_Data/5-1.Pasadena_zillow_data.csv')
Santaclarita_df=pd.read_csv('../Clean_Data/5-1.Santa Clarita_zillow_data.csv',encoding = "ISO-8859-1")
Torrance_df=pd.read_csv('../Clean_Data/5-1.Torrance_zillow_data.csv')

```


```python
# Combine all dataframe into one master dataframe
final_df = Burbank_df
final_df = final_df.append(Glendale_df, ignore_index=True)
final_df = final_df.append(Inglewood_df, ignore_index=True)
final_df = final_df.append(Alhambra_df, ignore_index=True)
final_df = final_df.append(Longbeach_df, ignore_index=True)
final_df = final_df.append(Losangeles_df, ignore_index=True)
final_df = final_df.append(Palmdale_df, ignore_index=True)
final_df = final_df.append(Pasadena_df, ignore_index=True)
final_df = final_df.append(Santaclarita_df, ignore_index=True)
final_df = final_df.append(Torrance_df, ignore_index=True)
final_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>20825166</td>
      <td>1010 Omer Ln</td>
      <td>Burbank CA 91502</td>
      <td>34.167726</td>
      <td>-118.305972</td>
      <td>0</td>
      <td>862895.0</td>
      <td>906040.0</td>
      <td>819750.0</td>
      <td>704,400</td>
      <td>378788.0</td>
      <td>2017</td>
      <td>1944.0</td>
      <td>6592</td>
      <td>1612.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>20065948</td>
      <td>2601 W Oak St</td>
      <td>Burbank CA 91505</td>
      <td>34.161428</td>
      <td>-118.331196</td>
      <td>0</td>
      <td>1064774.0</td>
      <td>1118013.0</td>
      <td>1011535.0</td>
      <td>704,400</td>
      <td>560430.0</td>
      <td>2017</td>
      <td>1977.0</td>
      <td>6267</td>
      <td>2161.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>20054209</td>
      <td>907 E Orange Grove Ave</td>
      <td>Burbank CA 91501</td>
      <td>34.190172</td>
      <td>-118.301154</td>
      <td>0</td>
      <td>816428.0</td>
      <td>857249.0</td>
      <td>775607.0</td>
      <td>704,400</td>
      <td>137700.0</td>
      <td>2017</td>
      <td>1938.0</td>
      <td>7453</td>
      <td>1006.0</td>
      <td>3.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>20049263</td>
      <td>214 S Lincoln St</td>
      <td>Burbank CA 91506</td>
      <td>34.161947</td>
      <td>-118.327251</td>
      <td>0</td>
      <td>758370.0</td>
      <td>796288.0</td>
      <td>720452.0</td>
      <td>704,400</td>
      <td>685000.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>7048</td>
      <td>1156.0</td>
      <td>2.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>20060944</td>
      <td>1600 Tulare Ave</td>
      <td>Burbank CA 91504</td>
      <td>34.202723</td>
      <td>-118.328088</td>
      <td>0</td>
      <td>820865.0</td>
      <td>861908.0</td>
      <td>779822.0</td>
      <td>704,400</td>
      <td>211628.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>8578</td>
      <td>1431.0</td>
      <td>2.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>20047601</td>
      <td>1516 N Lima St</td>
      <td>Burbank CA 91505</td>
      <td>34.178011</td>
      <td>-118.346856</td>
      <td>0</td>
      <td>703321.0</td>
      <td>738487.0</td>
      <td>668155.0</td>
      <td>704,400</td>
      <td>581981.0</td>
      <td>2017</td>
      <td>1940.0</td>
      <td>6882</td>
      <td>1200.0</td>
      <td>2.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>20057251</td>
      <td>2230 N Buena Vista St</td>
      <td>Burbank CA 91504</td>
      <td>34.197205</td>
      <td>-118.337743</td>
      <td>0</td>
      <td>654221.0</td>
      <td>686932.0</td>
      <td>621510.0</td>
      <td>704,400</td>
      <td>46412.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>6379</td>
      <td>924.0</td>
      <td>3.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>20055246</td>
      <td>532 Birmingham Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.196604</td>
      <td>-118.319713</td>
      <td>0</td>
      <td>868592.0</td>
      <td>912022.0</td>
      <td>825162.0</td>
      <td>704,400</td>
      <td>354264.0</td>
      <td>2017</td>
      <td>1951.0</td>
      <td>7262</td>
      <td>1332.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>20822902</td>
      <td>520 E Elmwood Ave</td>
      <td>Burbank CA 91501</td>
      <td>34.179782</td>
      <td>-118.297214</td>
      <td>0</td>
      <td>676454.0</td>
      <td>710277.0</td>
      <td>642631.0</td>
      <td>704,400</td>
      <td>254891.0</td>
      <td>2017</td>
      <td>1982.0</td>
      <td>23395</td>
      <td>1743.0</td>
      <td>2.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>20060170</td>
      <td>3425 Brace Canyon Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.217537</td>
      <td>-118.321944</td>
      <td>0</td>
      <td>1241727.0</td>
      <td>1365900.0</td>
      <td>1154806.0</td>
      <td>704,400</td>
      <td>675386.0</td>
      <td>2017</td>
      <td>1979.0</td>
      <td>10003</td>
      <td>2519.0</td>
      <td>3.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>20060426</td>
      <td>3421 Haven Way</td>
      <td>Burbank CA 91504</td>
      <td>34.210713</td>
      <td>-118.321536</td>
      <td>0</td>
      <td>1394567.0</td>
      <td>1492187.0</td>
      <td>1324839.0</td>
      <td>704,400</td>
      <td>849643.0</td>
      <td>2017</td>
      <td>1987.0</td>
      <td>13677</td>
      <td>2968.0</td>
      <td>4.0</td>
      <td>2.50</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>20051217</td>
      <td>1009 N Brighton St</td>
      <td>Burbank CA 91506</td>
      <td>34.177559</td>
      <td>-118.336548</td>
      <td>0</td>
      <td>825771.0</td>
      <td>867060.0</td>
      <td>784482.0</td>
      <td>704,400</td>
      <td>100728.0</td>
      <td>2017</td>
      <td>1929.0</td>
      <td>7198</td>
      <td>1565.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>20054592</td>
      <td>1018 E Verdugo Ave</td>
      <td>Burbank CA 91501</td>
      <td>34.188289</td>
      <td>-118.295140</td>
      <td>0</td>
      <td>825010.0</td>
      <td>866260.0</td>
      <td>783760.0</td>
      <td>704,400</td>
      <td>163842.0</td>
      <td>2017</td>
      <td>1924.0</td>
      <td>7622</td>
      <td>1128.0</td>
      <td>3.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>20033995</td>
      <td>9437 Via Monique</td>
      <td>Burbank CA 91504</td>
      <td>34.214276</td>
      <td>-118.338065</td>
      <td>0</td>
      <td>523220.0</td>
      <td>549381.0</td>
      <td>497059.0</td>
      <td>457,800</td>
      <td>212667.0</td>
      <td>2017</td>
      <td>1978.0</td>
      <td>195306</td>
      <td>1244.0</td>
      <td>2.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>20059331</td>
      <td>925 Uclan Dr</td>
      <td>Burbank CA 91504</td>
      <td>34.200128</td>
      <td>-118.313988</td>
      <td>0</td>
      <td>1320012.0</td>
      <td>1386013.0</td>
      <td>1254011.0</td>
      <td>704,400</td>
      <td>620006.0</td>
      <td>2017</td>
      <td>1951.0</td>
      <td>7380</td>
      <td>3464.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>20058053</td>
      <td>1801 N Kenneth Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.199918</td>
      <td>-118.318328</td>
      <td>0</td>
      <td>809373.0</td>
      <td>849842.0</td>
      <td>768904.0</td>
      <td>704,400</td>
      <td>467964.0</td>
      <td>2017</td>
      <td>1951.0</td>
      <td>6207</td>
      <td>1349.0</td>
      <td>3.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>20059627</td>
      <td>849 Stephen Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.204901</td>
      <td>-118.321313</td>
      <td>0</td>
      <td>1359750.0</td>
      <td>1441335.0</td>
      <td>1291763.0</td>
      <td>704,400</td>
      <td>655939.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>12918</td>
      <td>3106.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>20054059</td>
      <td>807 E Magnolia Blvd</td>
      <td>Burbank CA 91501</td>
      <td>34.190412</td>
      <td>-118.304481</td>
      <td>0</td>
      <td>1500091.0</td>
      <td>1605097.0</td>
      <td>1410086.0</td>
      <td>704,400</td>
      <td>1214679.0</td>
      <td>2017</td>
      <td>1990.0</td>
      <td>7548</td>
      <td>3510.0</td>
      <td>5.0</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>20064293</td>
      <td>3100 W Clark Ave</td>
      <td>Burbank CA 91505</td>
      <td>34.166079</td>
      <td>-118.339158</td>
      <td>0</td>
      <td>886086.0</td>
      <td>930390.0</td>
      <td>841782.0</td>
      <td>704,400</td>
      <td>483405.0</td>
      <td>2017</td>
      <td>1944.0</td>
      <td>8186</td>
      <td>1598.0</td>
      <td>3.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>20055053</td>
      <td>737 Tufts Ave</td>
      <td>Burbank CA 91504</td>
      <td>34.197743</td>
      <td>-118.315650</td>
      <td>0</td>
      <td>896872.0</td>
      <td>941716.0</td>
      <td>852028.0</td>
      <td>704,400</td>
      <td>610227.0</td>
      <td>2017</td>
      <td>1951.0</td>
      <td>6934</td>
      <td>1515.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>20051476</td>
      <td>910 N Orchard Dr</td>
      <td>Burbank CA 91506</td>
      <td>34.180284</td>
      <td>-118.330827</td>
      <td>0</td>
      <td>899636.0</td>
      <td>944618.0</td>
      <td>854654.0</td>
      <td>704,400</td>
      <td>421617.0</td>
      <td>2017</td>
      <td>1939.0</td>
      <td>5623</td>
      <td>1670.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>20060255</td>
      <td>2911 Joaquin Dr</td>
      <td>Burbank CA 91504</td>
      <td>34.210067</td>
      <td>-118.326065</td>
      <td>0</td>
      <td>1033467.0</td>
      <td>1085140.0</td>
      <td>981794.0</td>
      <td>704,400</td>
      <td>1159820.0</td>
      <td>2017</td>
      <td>1971.0</td>
      <td>7564</td>
      <td>2119.0</td>
      <td>4.0</td>
      <td>2.75</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>20058740</td>
      <td>1021 N Sunset Canyon Dr</td>
      <td>Burbank CA 91504</td>
      <td>34.199183</td>
      <td>-118.306176</td>
      <td>0</td>
      <td>1698486.0</td>
      <td>1783410.0</td>
      <td>1596577.0</td>
      <td>704,400</td>
      <td>1032448.0</td>
      <td>2017</td>
      <td>1958.0</td>
      <td>10018</td>
      <td>3644.0</td>
      <td>4.0</td>
      <td>5.00</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>20056484</td>
      <td>2120 N Screenland Dr</td>
      <td>Burbank CA 91505</td>
      <td>34.187495</td>
      <td>-118.351083</td>
      <td>0</td>
      <td>633986.0</td>
      <td>665685.0</td>
      <td>602287.0</td>
      <td>704,400</td>
      <td>398137.0</td>
      <td>2017</td>
      <td>1941.0</td>
      <td>6751</td>
      <td>918.0</td>
      <td>2.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>24</th>
      <td>24</td>
      <td>20049151</td>
      <td>201 S Orchard Dr</td>
      <td>Burbank CA 91506</td>
      <td>34.165746</td>
      <td>-118.323747</td>
      <td>0</td>
      <td>1041749.0</td>
      <td>1104254.0</td>
      <td>989662.0</td>
      <td>704,400</td>
      <td>504085.0</td>
      <td>2017</td>
      <td>1947.0</td>
      <td>9449</td>
      <td>2103.0</td>
      <td>2.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>20049707</td>
      <td>341 S Virginia Ave</td>
      <td>Burbank CA 91506</td>
      <td>34.166310</td>
      <td>-118.316893</td>
      <td>0</td>
      <td>878450.0</td>
      <td>922372.0</td>
      <td>834528.0</td>
      <td>704,400</td>
      <td>501798.0</td>
      <td>2017</td>
      <td>1944.0</td>
      <td>7463</td>
      <td>1597.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>20059572</td>
      <td>837 Stanford Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.203506</td>
      <td>-118.320289</td>
      <td>0</td>
      <td>937694.0</td>
      <td>984579.0</td>
      <td>890809.0</td>
      <td>704,400</td>
      <td>91156.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>8962</td>
      <td>1588.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>20059084</td>
      <td>936 Delaware Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.196666</td>
      <td>-118.308915</td>
      <td>0</td>
      <td>956943.0</td>
      <td>1004790.0</td>
      <td>909096.0</td>
      <td>704,400</td>
      <td>131576.0</td>
      <td>2017</td>
      <td>1952.0</td>
      <td>7429</td>
      <td>1671.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>28</th>
      <td>28</td>
      <td>20052423</td>
      <td>252 W Tujunga Ave</td>
      <td>Burbank CA 91502</td>
      <td>34.172590</td>
      <td>-118.313746</td>
      <td>0</td>
      <td>952454.0</td>
      <td>1000077.0</td>
      <td>904831.0</td>
      <td>704,400</td>
      <td>350542.0</td>
      <td>2017</td>
      <td>1925.0</td>
      <td>7749</td>
      <td>1912.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>29</th>
      <td>29</td>
      <td>20065394</td>
      <td>347 N Fairview St</td>
      <td>Burbank CA 91505</td>
      <td>34.161046</td>
      <td>-118.336985</td>
      <td>0</td>
      <td>1102554.0</td>
      <td>1157682.0</td>
      <td>1047426.0</td>
      <td>704,400</td>
      <td>887243.0</td>
      <td>2017</td>
      <td>1926.0</td>
      <td>6098</td>
      <td>2272.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>518</th>
      <td>22</td>
      <td>20373793</td>
      <td>3462 W 170th St</td>
      <td>Torrance CA 90504</td>
      <td>33.876746</td>
      <td>-118.332840</td>
      <td>0</td>
      <td>658930.0</td>
      <td>691876.0</td>
      <td>625984.0</td>
      <td>630,700</td>
      <td>298597.0</td>
      <td>2017</td>
      <td>1974.0</td>
      <td>116183</td>
      <td>1542.0</td>
      <td>3.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>519</th>
      <td>23</td>
      <td>20369587</td>
      <td>4033 184th St</td>
      <td>Torrance CA 90504</td>
      <td>33.864351</td>
      <td>-118.345436</td>
      <td>0</td>
      <td>762793.0</td>
      <td>800933.0</td>
      <td>724653.0</td>
      <td>630,700</td>
      <td>642702.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>5357</td>
      <td>1524.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>520</th>
      <td>24</td>
      <td>21267215</td>
      <td>21122 Harvard Blvd</td>
      <td>Torrance CA 90501</td>
      <td>33.837233</td>
      <td>-118.306409</td>
      <td>0</td>
      <td>559206.0</td>
      <td>587166.0</td>
      <td>531246.0</td>
      <td>459,700</td>
      <td>515000.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>8491</td>
      <td>1313.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>521</th>
      <td>25</td>
      <td>20373364</td>
      <td>17801 Glenburn Ave</td>
      <td>Torrance CA 90504</td>
      <td>33.869355</td>
      <td>-118.330599</td>
      <td>0</td>
      <td>710238.0</td>
      <td>745750.0</td>
      <td>674726.0</td>
      <td>630,700</td>
      <td>359565.0</td>
      <td>2017</td>
      <td>1955.0</td>
      <td>5300</td>
      <td>1249.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>522</th>
      <td>26</td>
      <td>21330789</td>
      <td>19417 Anza Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.853951</td>
      <td>-118.364198</td>
      <td>0</td>
      <td>797979.0</td>
      <td>837878.0</td>
      <td>758080.0</td>
      <td>798,600</td>
      <td>337061.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>5405</td>
      <td>1112.0</td>
      <td>3.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>523</th>
      <td>27</td>
      <td>21268629</td>
      <td>1551 W 206th St</td>
      <td>Torrance CA 90501</td>
      <td>33.844132</td>
      <td>-118.305907</td>
      <td>0</td>
      <td>562395.0</td>
      <td>590515.0</td>
      <td>528651.0</td>
      <td>459,700</td>
      <td>381971.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>7013</td>
      <td>1419.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>524</th>
      <td>28</td>
      <td>21327693</td>
      <td>5028 Lee St</td>
      <td>Torrance CA 90503</td>
      <td>33.835840</td>
      <td>-118.366641</td>
      <td>0</td>
      <td>1016519.0</td>
      <td>1067345.0</td>
      <td>965693.0</td>
      <td>809,400</td>
      <td>110872.0</td>
      <td>2017</td>
      <td>1956.0</td>
      <td>6760</td>
      <td>2075.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>525</th>
      <td>29</td>
      <td>21332168</td>
      <td>20357 Madison St</td>
      <td>Torrance CA 90503</td>
      <td>33.847001</td>
      <td>-118.348826</td>
      <td>0</td>
      <td>905076.0</td>
      <td>950330.0</td>
      <td>859822.0</td>
      <td>869,600</td>
      <td>772731.0</td>
      <td>2017</td>
      <td>1964.0</td>
      <td>6002</td>
      <td>2108.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>526</th>
      <td>30</td>
      <td>21267210</td>
      <td>21146 Harvard Blvd</td>
      <td>Torrance CA 90501</td>
      <td>33.837082</td>
      <td>-118.305997</td>
      <td>0</td>
      <td>674316.0</td>
      <td>708032.0</td>
      <td>640600.0</td>
      <td>459,700</td>
      <td>332782.0</td>
      <td>2017</td>
      <td>1953.0</td>
      <td>8491</td>
      <td>2404.0</td>
      <td>5.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>527</th>
      <td>31</td>
      <td>21265724</td>
      <td>1349 W 221st St</td>
      <td>Torrance CA 90501</td>
      <td>33.826921</td>
      <td>-118.301346</td>
      <td>0</td>
      <td>515391.0</td>
      <td>541161.0</td>
      <td>489621.0</td>
      <td>459,700</td>
      <td>251864.0</td>
      <td>2017</td>
      <td>1931.0</td>
      <td>6500</td>
      <td>754.0</td>
      <td>2.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>528</th>
      <td>32</td>
      <td>21330797</td>
      <td>5013 Deelane St</td>
      <td>Torrance CA 90503</td>
      <td>33.852527</td>
      <td>-118.363331</td>
      <td>0</td>
      <td>956409.0</td>
      <td>1004229.0</td>
      <td>908589.0</td>
      <td>798,600</td>
      <td>379003.0</td>
      <td>2017</td>
      <td>1955.0</td>
      <td>5701</td>
      <td>1792.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>529</th>
      <td>33</td>
      <td>21344235</td>
      <td>3399 Candlewood Rd</td>
      <td>Torrance CA 90505</td>
      <td>33.795606</td>
      <td>-118.347797</td>
      <td>0</td>
      <td>1021805.0</td>
      <td>1072895.0</td>
      <td>970715.0</td>
      <td>934,100</td>
      <td>478412.0</td>
      <td>2017</td>
      <td>1975.0</td>
      <td>5716</td>
      <td>2050.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>530</th>
      <td>34</td>
      <td>20376581</td>
      <td>18114 Manhattan Pl</td>
      <td>Torrance CA 90504</td>
      <td>33.865969</td>
      <td>-118.310153</td>
      <td>0</td>
      <td>656241.0</td>
      <td>689053.0</td>
      <td>623429.0</td>
      <td>613,300</td>
      <td>441464.0</td>
      <td>2017</td>
      <td>1981.0</td>
      <td>5812</td>
      <td>1918.0</td>
      <td>3.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>531</th>
      <td>35</td>
      <td>20374701</td>
      <td>17318 Casimir Ave</td>
      <td>Torrance CA 90504</td>
      <td>33.873867</td>
      <td>-118.321541</td>
      <td>0</td>
      <td>528203.0</td>
      <td>554613.0</td>
      <td>501793.0</td>
      <td>613,300</td>
      <td>461000.0</td>
      <td>2017</td>
      <td>1981.0</td>
      <td>176904</td>
      <td>1237.0</td>
      <td>2.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>532</th>
      <td>36</td>
      <td>82582698</td>
      <td>2365 Plaza del Amo</td>
      <td>Torrance CA 90501</td>
      <td>33.830503</td>
      <td>-118.322872</td>
      <td>0</td>
      <td>501828.0</td>
      <td>526919.0</td>
      <td>476737.0</td>
      <td>459,700</td>
      <td>441383.0</td>
      <td>2017</td>
      <td>2005.0</td>
      <td>43004</td>
      <td>1540.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>533</th>
      <td>37</td>
      <td>21333347</td>
      <td>21730 Ladeene Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.832560</td>
      <td>-118.359232</td>
      <td>0</td>
      <td>874133.0</td>
      <td>917840.0</td>
      <td>830426.0</td>
      <td>809,400</td>
      <td>654223.0</td>
      <td>2017</td>
      <td>1956.0</td>
      <td>6098</td>
      <td>1140.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>534</th>
      <td>38</td>
      <td>21282836</td>
      <td>3853 W 231st Pl</td>
      <td>Torrance CA 90505</td>
      <td>33.816568</td>
      <td>-118.353096</td>
      <td>0</td>
      <td>1039879.0</td>
      <td>1091873.0</td>
      <td>987885.0</td>
      <td>855,300</td>
      <td>481453.0</td>
      <td>2017</td>
      <td>1965.0</td>
      <td>6769</td>
      <td>2112.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>535</th>
      <td>39</td>
      <td>21344451</td>
      <td>3037 Lazy Meadow Dr</td>
      <td>Torrance CA 90505</td>
      <td>33.792223</td>
      <td>-118.342193</td>
      <td>0</td>
      <td>1096004.0</td>
      <td>1150804.0</td>
      <td>1041204.0</td>
      <td>934,100</td>
      <td>187574.0</td>
      <td>2017</td>
      <td>1975.0</td>
      <td>5713</td>
      <td>2561.0</td>
      <td>5.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>536</th>
      <td>40</td>
      <td>21326804</td>
      <td>5457-5465 Sharynne Ln</td>
      <td>Torrance CA 90505</td>
      <td>33.820220</td>
      <td>-118.373444</td>
      <td>0</td>
      <td>1712821.0</td>
      <td>1798462.0</td>
      <td>1627180.0</td>
      <td>869,800</td>
      <td>177135.0</td>
      <td>2017</td>
      <td>1947.0</td>
      <td>10977</td>
      <td>2557.0</td>
      <td>6.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>537</th>
      <td>41</td>
      <td>20372080</td>
      <td>18712 Felbar Ave</td>
      <td>Torrance CA 90504</td>
      <td>33.860539</td>
      <td>-118.338584</td>
      <td>0</td>
      <td>760967.0</td>
      <td>799015.0</td>
      <td>722919.0</td>
      <td>630,700</td>
      <td>198950.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>6897</td>
      <td>1541.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>538</th>
      <td>42</td>
      <td>21332980</td>
      <td>4298 Michelle Dr</td>
      <td>Torrance CA 90503</td>
      <td>33.846844</td>
      <td>-118.359318</td>
      <td>0</td>
      <td>1121540.0</td>
      <td>1177617.0</td>
      <td>1065463.0</td>
      <td>744,600</td>
      <td>335191.0</td>
      <td>2017</td>
      <td>1979.0</td>
      <td>6691</td>
      <td>2434.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>539</th>
      <td>43</td>
      <td>21332814</td>
      <td>21020 Ladeene Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.838877</td>
      <td>-118.360550</td>
      <td>0</td>
      <td>1572946.0</td>
      <td>1745970.0</td>
      <td>1447110.0</td>
      <td>744,600</td>
      <td>201902.0</td>
      <td>2017</td>
      <td>1963.0</td>
      <td>6290</td>
      <td>4271.0</td>
      <td>8.0</td>
      <td>6.00</td>
    </tr>
    <tr>
      <th>540</th>
      <td>44</td>
      <td>20372274</td>
      <td>3953 188th St</td>
      <td>Torrance CA 90504</td>
      <td>33.860355</td>
      <td>-118.343403</td>
      <td>0</td>
      <td>836513.0</td>
      <td>878339.0</td>
      <td>794687.0</td>
      <td>630,700</td>
      <td>537179.0</td>
      <td>2017</td>
      <td>1976.0</td>
      <td>6025</td>
      <td>2045.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>541</th>
      <td>45</td>
      <td>65249331</td>
      <td>4299 W 190th St</td>
      <td>Torrance CA 90504</td>
      <td>33.859246</td>
      <td>-118.349181</td>
      <td>0</td>
      <td>926908.0</td>
      <td>973253.0</td>
      <td>880563.0</td>
      <td>630,700</td>
      <td>710406.0</td>
      <td>2017</td>
      <td>2004.0</td>
      <td>131748</td>
      <td>2580.0</td>
      <td>4.0</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>542</th>
      <td>46</td>
      <td>21331622</td>
      <td>4729 Deelane St</td>
      <td>Torrance CA 90503</td>
      <td>33.852314</td>
      <td>-118.359005</td>
      <td>0</td>
      <td>932905.0</td>
      <td>979550.0</td>
      <td>886260.0</td>
      <td>798,600</td>
      <td>261643.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>5200</td>
      <td>1616.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>543</th>
      <td>47</td>
      <td>21271612</td>
      <td>2130 Plaza del Amo</td>
      <td>Torrance CA 90501</td>
      <td>33.826230</td>
      <td>-118.319730</td>
      <td>0</td>
      <td>610931.0</td>
      <td>641478.0</td>
      <td>580384.0</td>
      <td>595,500</td>
      <td>353851.0</td>
      <td>2017</td>
      <td>1979.0</td>
      <td>174102</td>
      <td>1490.0</td>
      <td>3.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>544</th>
      <td>48</td>
      <td>21278536</td>
      <td>2445 W 232nd St</td>
      <td>Torrance CA 90501</td>
      <td>33.815136</td>
      <td>-118.326792</td>
      <td>0</td>
      <td>1278215.0</td>
      <td>1342126.0</td>
      <td>1214304.0</td>
      <td>741,900</td>
      <td>565195.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>10149</td>
      <td>3578.0</td>
      <td>7.0</td>
      <td>5.00</td>
    </tr>
    <tr>
      <th>545</th>
      <td>49</td>
      <td>21276549</td>
      <td>3706 W 224th St</td>
      <td>Torrance CA 90505</td>
      <td>33.824205</td>
      <td>-118.348941</td>
      <td>0</td>
      <td>811534.0</td>
      <td>852111.0</td>
      <td>770957.0</td>
      <td>819,500</td>
      <td>592756.0</td>
      <td>2017</td>
      <td>1956.0</td>
      <td>5000</td>
      <td>1283.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>546</th>
      <td>50</td>
      <td>21336758</td>
      <td>4730 Newton St</td>
      <td>Torrance CA 90505</td>
      <td>33.807816</td>
      <td>-118.366960</td>
      <td>0</td>
      <td>1159646.0</td>
      <td>1217628.0</td>
      <td>1101664.0</td>
      <td>744,600</td>
      <td>286976.0</td>
      <td>2017</td>
      <td>1963.0</td>
      <td>8305</td>
      <td>1646.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>547</th>
      <td>51</td>
      <td>21327420</td>
      <td>21832 Barbara St</td>
      <td>Torrance CA 90503</td>
      <td>33.829898</td>
      <td>-118.374294</td>
      <td>0</td>
      <td>1263331.0</td>
      <td>1326498.0</td>
      <td>1200164.0</td>
      <td>809,400</td>
      <td>510994.0</td>
      <td>2017</td>
      <td>1955.0</td>
      <td>7227</td>
      <td>2321.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
  </tbody>
</table>
<p>548 rows × 18 columns</p>
</div>




```python
# reorder the columns
final_df = final_df[["zpid", "address","city_state_zip","latitude","longitude","message_code","zestimate",
               "valuation_high","valuation_low","home value index","tax assessment","tax assess year",
               "year built","lot size","finished sq ft","bedrooms","bathrooms"]]
# drop any NA/Null number/row
final_df = final_df.dropna(axis=0, how='any')
final_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20825166</td>
      <td>1010 Omer Ln</td>
      <td>Burbank CA 91502</td>
      <td>34.167726</td>
      <td>-118.305972</td>
      <td>0</td>
      <td>862895.0</td>
      <td>906040.0</td>
      <td>819750.0</td>
      <td>704,400</td>
      <td>378788.0</td>
      <td>2017</td>
      <td>1944.0</td>
      <td>6592</td>
      <td>1612.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20065948</td>
      <td>2601 W Oak St</td>
      <td>Burbank CA 91505</td>
      <td>34.161428</td>
      <td>-118.331196</td>
      <td>0</td>
      <td>1064774.0</td>
      <td>1118013.0</td>
      <td>1011535.0</td>
      <td>704,400</td>
      <td>560430.0</td>
      <td>2017</td>
      <td>1977.0</td>
      <td>6267</td>
      <td>2161.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20054209</td>
      <td>907 E Orange Grove Ave</td>
      <td>Burbank CA 91501</td>
      <td>34.190172</td>
      <td>-118.301154</td>
      <td>0</td>
      <td>816428.0</td>
      <td>857249.0</td>
      <td>775607.0</td>
      <td>704,400</td>
      <td>137700.0</td>
      <td>2017</td>
      <td>1938.0</td>
      <td>7453</td>
      <td>1006.0</td>
      <td>3.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20049263</td>
      <td>214 S Lincoln St</td>
      <td>Burbank CA 91506</td>
      <td>34.161947</td>
      <td>-118.327251</td>
      <td>0</td>
      <td>758370.0</td>
      <td>796288.0</td>
      <td>720452.0</td>
      <td>704,400</td>
      <td>685000.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>7048</td>
      <td>1156.0</td>
      <td>2.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20060944</td>
      <td>1600 Tulare Ave</td>
      <td>Burbank CA 91504</td>
      <td>34.202723</td>
      <td>-118.328088</td>
      <td>0</td>
      <td>820865.0</td>
      <td>861908.0</td>
      <td>779822.0</td>
      <td>704,400</td>
      <td>211628.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>8578</td>
      <td>1431.0</td>
      <td>2.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20047601</td>
      <td>1516 N Lima St</td>
      <td>Burbank CA 91505</td>
      <td>34.178011</td>
      <td>-118.346856</td>
      <td>0</td>
      <td>703321.0</td>
      <td>738487.0</td>
      <td>668155.0</td>
      <td>704,400</td>
      <td>581981.0</td>
      <td>2017</td>
      <td>1940.0</td>
      <td>6882</td>
      <td>1200.0</td>
      <td>2.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20057251</td>
      <td>2230 N Buena Vista St</td>
      <td>Burbank CA 91504</td>
      <td>34.197205</td>
      <td>-118.337743</td>
      <td>0</td>
      <td>654221.0</td>
      <td>686932.0</td>
      <td>621510.0</td>
      <td>704,400</td>
      <td>46412.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>6379</td>
      <td>924.0</td>
      <td>3.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>20055246</td>
      <td>532 Birmingham Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.196604</td>
      <td>-118.319713</td>
      <td>0</td>
      <td>868592.0</td>
      <td>912022.0</td>
      <td>825162.0</td>
      <td>704,400</td>
      <td>354264.0</td>
      <td>2017</td>
      <td>1951.0</td>
      <td>7262</td>
      <td>1332.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>8</th>
      <td>20822902</td>
      <td>520 E Elmwood Ave</td>
      <td>Burbank CA 91501</td>
      <td>34.179782</td>
      <td>-118.297214</td>
      <td>0</td>
      <td>676454.0</td>
      <td>710277.0</td>
      <td>642631.0</td>
      <td>704,400</td>
      <td>254891.0</td>
      <td>2017</td>
      <td>1982.0</td>
      <td>23395</td>
      <td>1743.0</td>
      <td>2.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>9</th>
      <td>20060170</td>
      <td>3425 Brace Canyon Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.217537</td>
      <td>-118.321944</td>
      <td>0</td>
      <td>1241727.0</td>
      <td>1365900.0</td>
      <td>1154806.0</td>
      <td>704,400</td>
      <td>675386.0</td>
      <td>2017</td>
      <td>1979.0</td>
      <td>10003</td>
      <td>2519.0</td>
      <td>3.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>20060426</td>
      <td>3421 Haven Way</td>
      <td>Burbank CA 91504</td>
      <td>34.210713</td>
      <td>-118.321536</td>
      <td>0</td>
      <td>1394567.0</td>
      <td>1492187.0</td>
      <td>1324839.0</td>
      <td>704,400</td>
      <td>849643.0</td>
      <td>2017</td>
      <td>1987.0</td>
      <td>13677</td>
      <td>2968.0</td>
      <td>4.0</td>
      <td>2.50</td>
    </tr>
    <tr>
      <th>11</th>
      <td>20051217</td>
      <td>1009 N Brighton St</td>
      <td>Burbank CA 91506</td>
      <td>34.177559</td>
      <td>-118.336548</td>
      <td>0</td>
      <td>825771.0</td>
      <td>867060.0</td>
      <td>784482.0</td>
      <td>704,400</td>
      <td>100728.0</td>
      <td>2017</td>
      <td>1929.0</td>
      <td>7198</td>
      <td>1565.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>12</th>
      <td>20054592</td>
      <td>1018 E Verdugo Ave</td>
      <td>Burbank CA 91501</td>
      <td>34.188289</td>
      <td>-118.295140</td>
      <td>0</td>
      <td>825010.0</td>
      <td>866260.0</td>
      <td>783760.0</td>
      <td>704,400</td>
      <td>163842.0</td>
      <td>2017</td>
      <td>1924.0</td>
      <td>7622</td>
      <td>1128.0</td>
      <td>3.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>13</th>
      <td>20033995</td>
      <td>9437 Via Monique</td>
      <td>Burbank CA 91504</td>
      <td>34.214276</td>
      <td>-118.338065</td>
      <td>0</td>
      <td>523220.0</td>
      <td>549381.0</td>
      <td>497059.0</td>
      <td>457,800</td>
      <td>212667.0</td>
      <td>2017</td>
      <td>1978.0</td>
      <td>195306</td>
      <td>1244.0</td>
      <td>2.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>14</th>
      <td>20059331</td>
      <td>925 Uclan Dr</td>
      <td>Burbank CA 91504</td>
      <td>34.200128</td>
      <td>-118.313988</td>
      <td>0</td>
      <td>1320012.0</td>
      <td>1386013.0</td>
      <td>1254011.0</td>
      <td>704,400</td>
      <td>620006.0</td>
      <td>2017</td>
      <td>1951.0</td>
      <td>7380</td>
      <td>3464.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>15</th>
      <td>20058053</td>
      <td>1801 N Kenneth Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.199918</td>
      <td>-118.318328</td>
      <td>0</td>
      <td>809373.0</td>
      <td>849842.0</td>
      <td>768904.0</td>
      <td>704,400</td>
      <td>467964.0</td>
      <td>2017</td>
      <td>1951.0</td>
      <td>6207</td>
      <td>1349.0</td>
      <td>3.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>16</th>
      <td>20059627</td>
      <td>849 Stephen Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.204901</td>
      <td>-118.321313</td>
      <td>0</td>
      <td>1359750.0</td>
      <td>1441335.0</td>
      <td>1291763.0</td>
      <td>704,400</td>
      <td>655939.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>12918</td>
      <td>3106.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>17</th>
      <td>20054059</td>
      <td>807 E Magnolia Blvd</td>
      <td>Burbank CA 91501</td>
      <td>34.190412</td>
      <td>-118.304481</td>
      <td>0</td>
      <td>1500091.0</td>
      <td>1605097.0</td>
      <td>1410086.0</td>
      <td>704,400</td>
      <td>1214679.0</td>
      <td>2017</td>
      <td>1990.0</td>
      <td>7548</td>
      <td>3510.0</td>
      <td>5.0</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>18</th>
      <td>20064293</td>
      <td>3100 W Clark Ave</td>
      <td>Burbank CA 91505</td>
      <td>34.166079</td>
      <td>-118.339158</td>
      <td>0</td>
      <td>886086.0</td>
      <td>930390.0</td>
      <td>841782.0</td>
      <td>704,400</td>
      <td>483405.0</td>
      <td>2017</td>
      <td>1944.0</td>
      <td>8186</td>
      <td>1598.0</td>
      <td>3.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>19</th>
      <td>20055053</td>
      <td>737 Tufts Ave</td>
      <td>Burbank CA 91504</td>
      <td>34.197743</td>
      <td>-118.315650</td>
      <td>0</td>
      <td>896872.0</td>
      <td>941716.0</td>
      <td>852028.0</td>
      <td>704,400</td>
      <td>610227.0</td>
      <td>2017</td>
      <td>1951.0</td>
      <td>6934</td>
      <td>1515.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20051476</td>
      <td>910 N Orchard Dr</td>
      <td>Burbank CA 91506</td>
      <td>34.180284</td>
      <td>-118.330827</td>
      <td>0</td>
      <td>899636.0</td>
      <td>944618.0</td>
      <td>854654.0</td>
      <td>704,400</td>
      <td>421617.0</td>
      <td>2017</td>
      <td>1939.0</td>
      <td>5623</td>
      <td>1670.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>21</th>
      <td>20060255</td>
      <td>2911 Joaquin Dr</td>
      <td>Burbank CA 91504</td>
      <td>34.210067</td>
      <td>-118.326065</td>
      <td>0</td>
      <td>1033467.0</td>
      <td>1085140.0</td>
      <td>981794.0</td>
      <td>704,400</td>
      <td>1159820.0</td>
      <td>2017</td>
      <td>1971.0</td>
      <td>7564</td>
      <td>2119.0</td>
      <td>4.0</td>
      <td>2.75</td>
    </tr>
    <tr>
      <th>22</th>
      <td>20058740</td>
      <td>1021 N Sunset Canyon Dr</td>
      <td>Burbank CA 91504</td>
      <td>34.199183</td>
      <td>-118.306176</td>
      <td>0</td>
      <td>1698486.0</td>
      <td>1783410.0</td>
      <td>1596577.0</td>
      <td>704,400</td>
      <td>1032448.0</td>
      <td>2017</td>
      <td>1958.0</td>
      <td>10018</td>
      <td>3644.0</td>
      <td>4.0</td>
      <td>5.00</td>
    </tr>
    <tr>
      <th>23</th>
      <td>20056484</td>
      <td>2120 N Screenland Dr</td>
      <td>Burbank CA 91505</td>
      <td>34.187495</td>
      <td>-118.351083</td>
      <td>0</td>
      <td>633986.0</td>
      <td>665685.0</td>
      <td>602287.0</td>
      <td>704,400</td>
      <td>398137.0</td>
      <td>2017</td>
      <td>1941.0</td>
      <td>6751</td>
      <td>918.0</td>
      <td>2.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>24</th>
      <td>20049151</td>
      <td>201 S Orchard Dr</td>
      <td>Burbank CA 91506</td>
      <td>34.165746</td>
      <td>-118.323747</td>
      <td>0</td>
      <td>1041749.0</td>
      <td>1104254.0</td>
      <td>989662.0</td>
      <td>704,400</td>
      <td>504085.0</td>
      <td>2017</td>
      <td>1947.0</td>
      <td>9449</td>
      <td>2103.0</td>
      <td>2.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>25</th>
      <td>20049707</td>
      <td>341 S Virginia Ave</td>
      <td>Burbank CA 91506</td>
      <td>34.166310</td>
      <td>-118.316893</td>
      <td>0</td>
      <td>878450.0</td>
      <td>922372.0</td>
      <td>834528.0</td>
      <td>704,400</td>
      <td>501798.0</td>
      <td>2017</td>
      <td>1944.0</td>
      <td>7463</td>
      <td>1597.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>26</th>
      <td>20059572</td>
      <td>837 Stanford Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.203506</td>
      <td>-118.320289</td>
      <td>0</td>
      <td>937694.0</td>
      <td>984579.0</td>
      <td>890809.0</td>
      <td>704,400</td>
      <td>91156.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>8962</td>
      <td>1588.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>27</th>
      <td>20059084</td>
      <td>936 Delaware Rd</td>
      <td>Burbank CA 91504</td>
      <td>34.196666</td>
      <td>-118.308915</td>
      <td>0</td>
      <td>956943.0</td>
      <td>1004790.0</td>
      <td>909096.0</td>
      <td>704,400</td>
      <td>131576.0</td>
      <td>2017</td>
      <td>1952.0</td>
      <td>7429</td>
      <td>1671.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>28</th>
      <td>20052423</td>
      <td>252 W Tujunga Ave</td>
      <td>Burbank CA 91502</td>
      <td>34.172590</td>
      <td>-118.313746</td>
      <td>0</td>
      <td>952454.0</td>
      <td>1000077.0</td>
      <td>904831.0</td>
      <td>704,400</td>
      <td>350542.0</td>
      <td>2017</td>
      <td>1925.0</td>
      <td>7749</td>
      <td>1912.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>29</th>
      <td>20065394</td>
      <td>347 N Fairview St</td>
      <td>Burbank CA 91505</td>
      <td>34.161046</td>
      <td>-118.336985</td>
      <td>0</td>
      <td>1102554.0</td>
      <td>1157682.0</td>
      <td>1047426.0</td>
      <td>704,400</td>
      <td>887243.0</td>
      <td>2017</td>
      <td>1926.0</td>
      <td>6098</td>
      <td>2272.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>518</th>
      <td>20373793</td>
      <td>3462 W 170th St</td>
      <td>Torrance CA 90504</td>
      <td>33.876746</td>
      <td>-118.332840</td>
      <td>0</td>
      <td>658930.0</td>
      <td>691876.0</td>
      <td>625984.0</td>
      <td>630,700</td>
      <td>298597.0</td>
      <td>2017</td>
      <td>1974.0</td>
      <td>116183</td>
      <td>1542.0</td>
      <td>3.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>519</th>
      <td>20369587</td>
      <td>4033 184th St</td>
      <td>Torrance CA 90504</td>
      <td>33.864351</td>
      <td>-118.345436</td>
      <td>0</td>
      <td>762793.0</td>
      <td>800933.0</td>
      <td>724653.0</td>
      <td>630,700</td>
      <td>642702.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>5357</td>
      <td>1524.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>520</th>
      <td>21267215</td>
      <td>21122 Harvard Blvd</td>
      <td>Torrance CA 90501</td>
      <td>33.837233</td>
      <td>-118.306409</td>
      <td>0</td>
      <td>559206.0</td>
      <td>587166.0</td>
      <td>531246.0</td>
      <td>459,700</td>
      <td>515000.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>8491</td>
      <td>1313.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>521</th>
      <td>20373364</td>
      <td>17801 Glenburn Ave</td>
      <td>Torrance CA 90504</td>
      <td>33.869355</td>
      <td>-118.330599</td>
      <td>0</td>
      <td>710238.0</td>
      <td>745750.0</td>
      <td>674726.0</td>
      <td>630,700</td>
      <td>359565.0</td>
      <td>2017</td>
      <td>1955.0</td>
      <td>5300</td>
      <td>1249.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>522</th>
      <td>21330789</td>
      <td>19417 Anza Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.853951</td>
      <td>-118.364198</td>
      <td>0</td>
      <td>797979.0</td>
      <td>837878.0</td>
      <td>758080.0</td>
      <td>798,600</td>
      <td>337061.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>5405</td>
      <td>1112.0</td>
      <td>3.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>523</th>
      <td>21268629</td>
      <td>1551 W 206th St</td>
      <td>Torrance CA 90501</td>
      <td>33.844132</td>
      <td>-118.305907</td>
      <td>0</td>
      <td>562395.0</td>
      <td>590515.0</td>
      <td>528651.0</td>
      <td>459,700</td>
      <td>381971.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>7013</td>
      <td>1419.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>524</th>
      <td>21327693</td>
      <td>5028 Lee St</td>
      <td>Torrance CA 90503</td>
      <td>33.835840</td>
      <td>-118.366641</td>
      <td>0</td>
      <td>1016519.0</td>
      <td>1067345.0</td>
      <td>965693.0</td>
      <td>809,400</td>
      <td>110872.0</td>
      <td>2017</td>
      <td>1956.0</td>
      <td>6760</td>
      <td>2075.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>525</th>
      <td>21332168</td>
      <td>20357 Madison St</td>
      <td>Torrance CA 90503</td>
      <td>33.847001</td>
      <td>-118.348826</td>
      <td>0</td>
      <td>905076.0</td>
      <td>950330.0</td>
      <td>859822.0</td>
      <td>869,600</td>
      <td>772731.0</td>
      <td>2017</td>
      <td>1964.0</td>
      <td>6002</td>
      <td>2108.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>526</th>
      <td>21267210</td>
      <td>21146 Harvard Blvd</td>
      <td>Torrance CA 90501</td>
      <td>33.837082</td>
      <td>-118.305997</td>
      <td>0</td>
      <td>674316.0</td>
      <td>708032.0</td>
      <td>640600.0</td>
      <td>459,700</td>
      <td>332782.0</td>
      <td>2017</td>
      <td>1953.0</td>
      <td>8491</td>
      <td>2404.0</td>
      <td>5.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>527</th>
      <td>21265724</td>
      <td>1349 W 221st St</td>
      <td>Torrance CA 90501</td>
      <td>33.826921</td>
      <td>-118.301346</td>
      <td>0</td>
      <td>515391.0</td>
      <td>541161.0</td>
      <td>489621.0</td>
      <td>459,700</td>
      <td>251864.0</td>
      <td>2017</td>
      <td>1931.0</td>
      <td>6500</td>
      <td>754.0</td>
      <td>2.0</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>528</th>
      <td>21330797</td>
      <td>5013 Deelane St</td>
      <td>Torrance CA 90503</td>
      <td>33.852527</td>
      <td>-118.363331</td>
      <td>0</td>
      <td>956409.0</td>
      <td>1004229.0</td>
      <td>908589.0</td>
      <td>798,600</td>
      <td>379003.0</td>
      <td>2017</td>
      <td>1955.0</td>
      <td>5701</td>
      <td>1792.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>529</th>
      <td>21344235</td>
      <td>3399 Candlewood Rd</td>
      <td>Torrance CA 90505</td>
      <td>33.795606</td>
      <td>-118.347797</td>
      <td>0</td>
      <td>1021805.0</td>
      <td>1072895.0</td>
      <td>970715.0</td>
      <td>934,100</td>
      <td>478412.0</td>
      <td>2017</td>
      <td>1975.0</td>
      <td>5716</td>
      <td>2050.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>530</th>
      <td>20376581</td>
      <td>18114 Manhattan Pl</td>
      <td>Torrance CA 90504</td>
      <td>33.865969</td>
      <td>-118.310153</td>
      <td>0</td>
      <td>656241.0</td>
      <td>689053.0</td>
      <td>623429.0</td>
      <td>613,300</td>
      <td>441464.0</td>
      <td>2017</td>
      <td>1981.0</td>
      <td>5812</td>
      <td>1918.0</td>
      <td>3.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>531</th>
      <td>20374701</td>
      <td>17318 Casimir Ave</td>
      <td>Torrance CA 90504</td>
      <td>33.873867</td>
      <td>-118.321541</td>
      <td>0</td>
      <td>528203.0</td>
      <td>554613.0</td>
      <td>501793.0</td>
      <td>613,300</td>
      <td>461000.0</td>
      <td>2017</td>
      <td>1981.0</td>
      <td>176904</td>
      <td>1237.0</td>
      <td>2.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>532</th>
      <td>82582698</td>
      <td>2365 Plaza del Amo</td>
      <td>Torrance CA 90501</td>
      <td>33.830503</td>
      <td>-118.322872</td>
      <td>0</td>
      <td>501828.0</td>
      <td>526919.0</td>
      <td>476737.0</td>
      <td>459,700</td>
      <td>441383.0</td>
      <td>2017</td>
      <td>2005.0</td>
      <td>43004</td>
      <td>1540.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>533</th>
      <td>21333347</td>
      <td>21730 Ladeene Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.832560</td>
      <td>-118.359232</td>
      <td>0</td>
      <td>874133.0</td>
      <td>917840.0</td>
      <td>830426.0</td>
      <td>809,400</td>
      <td>654223.0</td>
      <td>2017</td>
      <td>1956.0</td>
      <td>6098</td>
      <td>1140.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>534</th>
      <td>21282836</td>
      <td>3853 W 231st Pl</td>
      <td>Torrance CA 90505</td>
      <td>33.816568</td>
      <td>-118.353096</td>
      <td>0</td>
      <td>1039879.0</td>
      <td>1091873.0</td>
      <td>987885.0</td>
      <td>855,300</td>
      <td>481453.0</td>
      <td>2017</td>
      <td>1965.0</td>
      <td>6769</td>
      <td>2112.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>535</th>
      <td>21344451</td>
      <td>3037 Lazy Meadow Dr</td>
      <td>Torrance CA 90505</td>
      <td>33.792223</td>
      <td>-118.342193</td>
      <td>0</td>
      <td>1096004.0</td>
      <td>1150804.0</td>
      <td>1041204.0</td>
      <td>934,100</td>
      <td>187574.0</td>
      <td>2017</td>
      <td>1975.0</td>
      <td>5713</td>
      <td>2561.0</td>
      <td>5.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>536</th>
      <td>21326804</td>
      <td>5457-5465 Sharynne Ln</td>
      <td>Torrance CA 90505</td>
      <td>33.820220</td>
      <td>-118.373444</td>
      <td>0</td>
      <td>1712821.0</td>
      <td>1798462.0</td>
      <td>1627180.0</td>
      <td>869,800</td>
      <td>177135.0</td>
      <td>2017</td>
      <td>1947.0</td>
      <td>10977</td>
      <td>2557.0</td>
      <td>6.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>537</th>
      <td>20372080</td>
      <td>18712 Felbar Ave</td>
      <td>Torrance CA 90504</td>
      <td>33.860539</td>
      <td>-118.338584</td>
      <td>0</td>
      <td>760967.0</td>
      <td>799015.0</td>
      <td>722919.0</td>
      <td>630,700</td>
      <td>198950.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>6897</td>
      <td>1541.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>538</th>
      <td>21332980</td>
      <td>4298 Michelle Dr</td>
      <td>Torrance CA 90503</td>
      <td>33.846844</td>
      <td>-118.359318</td>
      <td>0</td>
      <td>1121540.0</td>
      <td>1177617.0</td>
      <td>1065463.0</td>
      <td>744,600</td>
      <td>335191.0</td>
      <td>2017</td>
      <td>1979.0</td>
      <td>6691</td>
      <td>2434.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>539</th>
      <td>21332814</td>
      <td>21020 Ladeene Ave</td>
      <td>Torrance CA 90503</td>
      <td>33.838877</td>
      <td>-118.360550</td>
      <td>0</td>
      <td>1572946.0</td>
      <td>1745970.0</td>
      <td>1447110.0</td>
      <td>744,600</td>
      <td>201902.0</td>
      <td>2017</td>
      <td>1963.0</td>
      <td>6290</td>
      <td>4271.0</td>
      <td>8.0</td>
      <td>6.00</td>
    </tr>
    <tr>
      <th>540</th>
      <td>20372274</td>
      <td>3953 188th St</td>
      <td>Torrance CA 90504</td>
      <td>33.860355</td>
      <td>-118.343403</td>
      <td>0</td>
      <td>836513.0</td>
      <td>878339.0</td>
      <td>794687.0</td>
      <td>630,700</td>
      <td>537179.0</td>
      <td>2017</td>
      <td>1976.0</td>
      <td>6025</td>
      <td>2045.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>541</th>
      <td>65249331</td>
      <td>4299 W 190th St</td>
      <td>Torrance CA 90504</td>
      <td>33.859246</td>
      <td>-118.349181</td>
      <td>0</td>
      <td>926908.0</td>
      <td>973253.0</td>
      <td>880563.0</td>
      <td>630,700</td>
      <td>710406.0</td>
      <td>2017</td>
      <td>2004.0</td>
      <td>131748</td>
      <td>2580.0</td>
      <td>4.0</td>
      <td>4.00</td>
    </tr>
    <tr>
      <th>542</th>
      <td>21331622</td>
      <td>4729 Deelane St</td>
      <td>Torrance CA 90503</td>
      <td>33.852314</td>
      <td>-118.359005</td>
      <td>0</td>
      <td>932905.0</td>
      <td>979550.0</td>
      <td>886260.0</td>
      <td>798,600</td>
      <td>261643.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>5200</td>
      <td>1616.0</td>
      <td>3.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>543</th>
      <td>21271612</td>
      <td>2130 Plaza del Amo</td>
      <td>Torrance CA 90501</td>
      <td>33.826230</td>
      <td>-118.319730</td>
      <td>0</td>
      <td>610931.0</td>
      <td>641478.0</td>
      <td>580384.0</td>
      <td>595,500</td>
      <td>353851.0</td>
      <td>2017</td>
      <td>1979.0</td>
      <td>174102</td>
      <td>1490.0</td>
      <td>3.0</td>
      <td>3.00</td>
    </tr>
    <tr>
      <th>544</th>
      <td>21278536</td>
      <td>2445 W 232nd St</td>
      <td>Torrance CA 90501</td>
      <td>33.815136</td>
      <td>-118.326792</td>
      <td>0</td>
      <td>1278215.0</td>
      <td>1342126.0</td>
      <td>1214304.0</td>
      <td>741,900</td>
      <td>565195.0</td>
      <td>2017</td>
      <td>1954.0</td>
      <td>10149</td>
      <td>3578.0</td>
      <td>7.0</td>
      <td>5.00</td>
    </tr>
    <tr>
      <th>545</th>
      <td>21276549</td>
      <td>3706 W 224th St</td>
      <td>Torrance CA 90505</td>
      <td>33.824205</td>
      <td>-118.348941</td>
      <td>0</td>
      <td>811534.0</td>
      <td>852111.0</td>
      <td>770957.0</td>
      <td>819,500</td>
      <td>592756.0</td>
      <td>2017</td>
      <td>1956.0</td>
      <td>5000</td>
      <td>1283.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>546</th>
      <td>21336758</td>
      <td>4730 Newton St</td>
      <td>Torrance CA 90505</td>
      <td>33.807816</td>
      <td>-118.366960</td>
      <td>0</td>
      <td>1159646.0</td>
      <td>1217628.0</td>
      <td>1101664.0</td>
      <td>744,600</td>
      <td>286976.0</td>
      <td>2017</td>
      <td>1963.0</td>
      <td>8305</td>
      <td>1646.0</td>
      <td>4.0</td>
      <td>2.00</td>
    </tr>
    <tr>
      <th>547</th>
      <td>21327420</td>
      <td>21832 Barbara St</td>
      <td>Torrance CA 90503</td>
      <td>33.829898</td>
      <td>-118.374294</td>
      <td>0</td>
      <td>1263331.0</td>
      <td>1326498.0</td>
      <td>1200164.0</td>
      <td>809,400</td>
      <td>510994.0</td>
      <td>2017</td>
      <td>1955.0</td>
      <td>7227</td>
      <td>2321.0</td>
      <td>4.0</td>
      <td>3.00</td>
    </tr>
  </tbody>
</table>
<p>545 rows × 17 columns</p>
</div>




```python
#add in new columns to store new values
final_df['rentzestimate'] =''
final_df['valuechange'] =''
final_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
      <th>rentzestimate</th>
      <th>valuechange</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20825166</td>
      <td>1010 Omer Ln</td>
      <td>Burbank CA 91502</td>
      <td>34.167726</td>
      <td>-118.305972</td>
      <td>0</td>
      <td>862895.0</td>
      <td>906040.0</td>
      <td>819750.0</td>
      <td>704,400</td>
      <td>378788.0</td>
      <td>2017</td>
      <td>1944.0</td>
      <td>6592</td>
      <td>1612.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>1</th>
      <td>20065948</td>
      <td>2601 W Oak St</td>
      <td>Burbank CA 91505</td>
      <td>34.161428</td>
      <td>-118.331196</td>
      <td>0</td>
      <td>1064774.0</td>
      <td>1118013.0</td>
      <td>1011535.0</td>
      <td>704,400</td>
      <td>560430.0</td>
      <td>2017</td>
      <td>1977.0</td>
      <td>6267</td>
      <td>2161.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>2</th>
      <td>20054209</td>
      <td>907 E Orange Grove Ave</td>
      <td>Burbank CA 91501</td>
      <td>34.190172</td>
      <td>-118.301154</td>
      <td>0</td>
      <td>816428.0</td>
      <td>857249.0</td>
      <td>775607.0</td>
      <td>704,400</td>
      <td>137700.0</td>
      <td>2017</td>
      <td>1938.0</td>
      <td>7453</td>
      <td>1006.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>3</th>
      <td>20049263</td>
      <td>214 S Lincoln St</td>
      <td>Burbank CA 91506</td>
      <td>34.161947</td>
      <td>-118.327251</td>
      <td>0</td>
      <td>758370.0</td>
      <td>796288.0</td>
      <td>720452.0</td>
      <td>704,400</td>
      <td>685000.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>7048</td>
      <td>1156.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>20060944</td>
      <td>1600 Tulare Ave</td>
      <td>Burbank CA 91504</td>
      <td>34.202723</td>
      <td>-118.328088</td>
      <td>0</td>
      <td>820865.0</td>
      <td>861908.0</td>
      <td>779822.0</td>
      <td>704,400</td>
      <td>211628.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>8578</td>
      <td>1431.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>
</div>




```python
# define function to pull 30 day value change and rentestimate
def search_zillow(df):
    
    for index, row in df.iterrows():
        try:
            url = 'https://www.zillow.com/webservice/GetDeepSearchResults.htm?zws-id='
            address = df['address'][index]
            citystatezip = df['city_state_zip'][index]


            query_url = url + zws_id + '&address=' + urllib.parse.quote(address) + '&citystatezip=' + urllib.parse.quote(citystatezip) +'&rentzestimate=true' 


            root = ET.parse(urlopen(query_url)).getroot()

            print("row " + format(index) + ": " + address + citystatezip)
            

            #30dayvaluechange
            for zestimate in root.iter('zestimate'):
                valuechange_value = zestimate[3].text

                if valuechange_value is None:
                    print('not available')
                else:
                    print ('30 day value change: ' + format(zestimate[3].text)) 
                    df.set_value(index, 'valuechange', valuechange_value)
                    
            #rentzestimate
            for rentzestimate in root.iter('rentzestimate'):
                rentzestimate_value = rentzestimate[0].text

                if rentzestimate_value is None:
                    print('not for rent')
                else:
                    print ('rentzestimate (value): ' + format(rentzestimate[0].text)) 
                    df.set_value(index, 'rentzestimate', rentzestimate_value)
            
            print('\n')

            time.sleep(0.5) 


        except:
            break
```


```python
#use function to pull rent estimate and 30 day price change
search_zillow(final_df)
```

    row 0: 1010 Omer Ln Burbank CA 91502
    30 day value change: 23936
    rentzestimate (value): 2500
    
    
    row 1: 2601 W Oak St Burbank CA 91505
    30 day value change: 40688
    rentzestimate (value): 3900
    
    
    row 2: 907 E Orange Grove Ave Burbank CA 91501
    30 day value change: 18408
    rentzestimate (value): 2800
    
    
    row 3: 214 S Lincoln St Burbank CA 91506
    30 day value change: -2574
    rentzestimate (value): 2950
    
    
    row 4: 1600 Tulare Ave Burbank CA 91504
    30 day value change: -786
    rentzestimate (value): 3100
    
    
    row 5: 1516 N Lima St Burbank CA 91505
    30 day value change: 22662
    rentzestimate (value): 3200
    
    
    row 6: 2230 N Buena Vista St Burbank CA 91504
    30 day value change: 13237
    rentzestimate (value): 2700
    
    
    row 7: 532 Birmingham Rd Burbank CA 91504
    30 day value change: 9215
    rentzestimate (value): 3200
    
    
    row 8: 520 E Elmwood Ave Burbank CA 91501
    30 day value change: 10864
    rentzestimate (value): 3200
    
    
    row 9: 3425 Brace Canyon Rd Burbank CA 91504
    30 day value change: -10305
    rentzestimate (value): 4500
    
    
    row 10: 3421 Haven Way Burbank CA 91504
    30 day value change: 17909
    rentzestimate (value): 5500
    
    
    row 11: 1009 N Brighton St Burbank CA 91506
    30 day value change: 11623
    rentzestimate (value): 3150
    
    
    row 12: 1018 E Verdugo Ave Burbank CA 91501
    30 day value change: 5448
    rentzestimate (value): 2800
    
    
    row 13: 9437 Via Monique Burbank CA 91504
    30 day value change: 9013
    rentzestimate (value): 3000
    
    
    row 14: 925 Uclan Dr Burbank CA 91504
    30 day value change: 10866
    rentzestimate (value): 4500
    
    
    row 15: 1801 N Kenneth Rd Burbank CA 91504
    30 day value change: 4367
    rentzestimate (value): 3200
    
    
    row 16: 849 Stephen Rd Burbank CA 91504
    30 day value change: 16481
    rentzestimate (value): 5000
    
    
    row 17: 807 E Magnolia Blvd Burbank CA 91501
    30 day value change: 43410
    rentzestimate (value): 6500
    
    
    row 18: 3100 W Clark Ave Burbank CA 91505
    30 day value change: -1600
    rentzestimate (value): 3300
    
    
    row 19: 737 Tufts Ave Burbank CA 91504
    30 day value change: 11211
    rentzestimate (value): 3595
    
    
    row 20: 910 N Orchard Dr Burbank CA 91506
    30 day value change: 14633
    rentzestimate (value): 3475
    
    
    row 21: 2911 Joaquin Dr Burbank CA 91504
    30 day value change: -1941
    rentzestimate (value): 3800
    
    
    row 22: 1021 N Sunset Canyon Dr Burbank CA 91504
    30 day value change: 123471
    rentzestimate (value): 5815
    
    
    row 23: 2120 N Screenland Dr Burbank CA 91505
    30 day value change: 11423
    rentzestimate (value): 2900
    
    
    row 24: 201 S Orchard Dr Burbank CA 91506
    30 day value change: 28273
    rentzestimate (value): 3800
    
    
    row 25: 341 S Virginia Ave Burbank CA 91506
    30 day value change: 9019
    rentzestimate (value): 3495
    
    
    row 26: 837 Stanford Rd Burbank CA 91504
    30 day value change: 3432
    rentzestimate (value): 3500
    
    
    row 27: 936 Delaware Rd Burbank CA 91504
    30 day value change: 10880
    rentzestimate (value): 3500
    
    
    row 28: 252 W Tujunga Ave Burbank CA 91502
    30 day value change: -15727
    rentzestimate (value): 2500
    
    
    row 29: 347 N Fairview St Burbank CA 91505
    30 day value change: 21824
    rentzestimate (value): 3823
    
    
    row 30: 1899 Thurber Pl Burbank CA 91501
    30 day value change: 11542
    rentzestimate (value): 3900
    
    
    row 31: 1209 E Elmwood Ave Burbank CA 91501
    30 day value change: 29477
    rentzestimate (value): 15626
    
    
    row 32: 2333 N Catalina St Burbank CA 91504
    30 day value change: -9704
    rentzestimate (value): 3200
    
    
    row 33: 230 N California St Burbank CA 91505
    30 day value change: 6921
    rentzestimate (value): 3200
    
    
    row 34: 2621 N Myers St Burbank CA 91504
    30 day value change: 7437
    rentzestimate (value): 3150
    
    
    row 35: 1899 Thurber Pl Burbank CA 91501
    30 day value change: 11542
    rentzestimate (value): 3900
    
    
    row 36: 1211 N Sparks St Burbank CA 91506
    30 day value change: 9573
    rentzestimate (value): 2800
    
    
    row 37: 1818 Karen St Burbank CA 91504
    30 day value change: 1225
    rentzestimate (value): 3500
    
    
    row 38: 316 N Florence St Burbank CA 91505
    30 day value change: 34050
    rentzestimate (value): 2800
    
    
    row 39: 824 S Bel Aire Dr Burbank CA 91501
    30 day value change: 4929
    rentzestimate (value): 3800
    
    
    row 40: 1715 Rudell Rd Burbank CA 91501
    30 day value change: -4451
    rentzestimate (value): 9367
    
    
    row 41: 3434 Viewcrest Dr Burbank CA 91504
    30 day value change: 42640
    rentzestimate (value): 6993
    
    
    row 42: 3421 Kildare Ct Burbank CA 91504
    30 day value change: -96786
    rentzestimate (value): 8350
    
    
    row 43: 618 N Beachwood Dr Burbank CA 91506
    30 day value change: -13084
    rentzestimate (value): 3295
    
    
    row 44: 634 N Parish Pl Burbank CA 91506
    30 day value change: 18039
    rentzestimate (value): 3200
    
    
    row 45: 1612 N Pepper St Burbank CA 91505
    30 day value change: 10177
    rentzestimate (value): 3195
    
    
    row 46: 544 N Lincoln St Burbank CA 91506
    30 day value change: 11032
    30 day value change: 11879
    rentzestimate (value): 2850
    
    
    row 47: 1620 N San Fernando Blvd Burbank CA 91504
    30 day value change: 6195
    30 day value change: 2421
    30 day value change: 3464
    30 day value change: 7318
    30 day value change: 957
    30 day value change: 4568
    30 day value change: -226
    30 day value change: 6613
    30 day value change: 2406
    30 day value change: 5175
    30 day value change: 3495
    30 day value change: 3190
    30 day value change: 123
    30 day value change: -4579
    30 day value change: 3593
    30 day value change: 4707
    30 day value change: -3142
    30 day value change: 1609
    30 day value change: 2060
    30 day value change: 257
    30 day value change: 3421
    30 day value change: 4701
    30 day value change: 5101
    30 day value change: 446
    30 day value change: 4676
    rentzestimate (value): 2200
    rentzestimate (value): 2300
    rentzestimate (value): 2345
    rentzestimate (value): 2300
    rentzestimate (value): 2250
    rentzestimate (value): 2250
    rentzestimate (value): 2300
    rentzestimate (value): 2200
    rentzestimate (value): 2300
    rentzestimate (value): 2200
    rentzestimate (value): 2300
    rentzestimate (value): 2475
    rentzestimate (value): 2300
    rentzestimate (value): 2255
    rentzestimate (value): 2300
    rentzestimate (value): 2295
    rentzestimate (value): 2300
    rentzestimate (value): 2449
    rentzestimate (value): 2300
    rentzestimate (value): 2250
    rentzestimate (value): 2345
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2300
    rentzestimate (value): 2200
    
    
    row 48: 456 E San Jose Ave Burbank CA 91501
    30 day value change: 13176
    rentzestimate (value): 2545
    
    
    row 49: 1209 E Elmwood Ave Burbank CA 91501
    30 day value change: 29477
    rentzestimate (value): 15626
    
    
    row 50: 1914 Landis St Burbank CA 91504
    30 day value change: 14644
    rentzestimate (value): 2450
    
    
    row 51: 2204 Peyton Ave Burbank CA 91504
    30 day value change: 5695
    rentzestimate (value): 2600
    
    
    row 52: Bicycle Path Los Angeles CA 90039
    
    
    row 53: 1848 Sherer Ln Glendale CA 91208
    30 day value change: 52752
    rentzestimate (value): 4534
    
    
    row 54: 1914 Polaris Dr Glendale CA 91208
    30 day value change: 17236
    rentzestimate (value): 3570
    
    
    row 55: 606 South St Glendale CA 91202
    30 day value change: -12388
    rentzestimate (value): 2750
    
    
    row 56: 1412 Lake St Glendale CA 91201
    30 day value change: 6975
    rentzestimate (value): 3000
    
    
    row 57: 730 Patterson Ave Glendale CA 91202
    30 day value change: 9868
    rentzestimate (value): 3250
    
    
    row 58: 2242 E Chevy Chase Dr Glendale CA 91206
    30 day value change: -16440
    rentzestimate (value): 3300
    
    
    row 59: 1314 Norton Ave Glendale CA 91202
    30 day value change: 8579
    rentzestimate (value): 3650
    
    
    row 60: 1201 E Broadway Glendale CA 91205
    30 day value change: 13055
    rentzestimate (value): 2500
    
    
    row 61: 1510 Virginia Ave Glendale CA 91202
    30 day value change: 32960
    rentzestimate (value): 4950
    
    
    row 62: 826 N Glendale Ave Glendale CA 91206
    30 day value change: 2811
    rentzestimate (value): 2695
    
    
    row 63: CA-2 Glendale CA
    30 day value change: -3188
    30 day value change: 35082
    30 day value change: -76894
    30 day value change: -35239
    30 day value change: 33930
    30 day value change: 6161
    30 day value change: 8333
    30 day value change: 1418
    30 day value change: -90955
    30 day value change: 29638
    30 day value change: 9200
    30 day value change: 4863
    rentzestimate (value): 2300
    rentzestimate (value): 2400
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 3000
    rentzestimate (value): 3000
    rentzestimate (value): 2550
    rentzestimate (value): 2350
    rentzestimate (value): 2250
    rentzestimate (value): 1850
    rentzestimate (value): 2400
    rentzestimate (value): 2650
    
    
    row 64: 900 Calle Del Pacifico Glendale CA 91208
    30 day value change: 15571
    rentzestimate (value): 4303
    
    
    row 65: 1201 Oakridge Dr Glendale CA 91205
    30 day value change: 4504
    rentzestimate (value): 2995
    
    
    row 66: 405 Chester St Glendale CA 91203
    30 day value change: 41535
    rentzestimate (value): 3750
    
    
    row 67: 516 W Stocker St Glendale CA 91202
    30 day value change: 20069
    rentzestimate (value): 2895
    
    
    row 68: 418 Ross St Glendale CA 91207
    30 day value change: 19043
    rentzestimate (value): 3506
    
    
    row 69: 1530 Arboles Dr Glendale CA 91207
    30 day value change: -10172
    rentzestimate (value): 4327
    
    
    row 70: 612 N Louise St Glendale CA 91206
    30 day value change: 11783
    30 day value change: 7751
    30 day value change: 2599
    30 day value change: 9068
    30 day value change: 12606
    30 day value change: 14586
    30 day value change: 336
    30 day value change: 9499
    30 day value change: 4694
    30 day value change: 10643
    30 day value change: 8362
    30 day value change: 10761
    30 day value change: 352
    30 day value change: 11147
    30 day value change: 8122
    rentzestimate (value): 2350
    rentzestimate (value): 2650
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2400
    rentzestimate (value): 2300
    rentzestimate (value): 2200
    rentzestimate (value): 2600
    rentzestimate (value): 2276
    rentzestimate (value): 2350
    rentzestimate (value): 2550
    rentzestimate (value): 2395
    rentzestimate (value): 2200
    rentzestimate (value): 2495
    rentzestimate (value): 2400
    
    
    row 71: 863 Harrington Rd Glendale CA 91207
    30 day value change: -9555
    rentzestimate (value): 4532
    
    
    row 72: 1333 Rossmoyne Ave Glendale CA 91207
    30 day value change: 51792
    rentzestimate (value): 4174
    
    
    row 73: 264 W Kenneth Rd Glendale CA 91202
    30 day value change: 10108
    rentzestimate (value): 3800
    
    
    row 74: 310 Wonderview Dr Glendale CA 91202
    30 day value change: 114078
    rentzestimate (value): 5000
    
    
    row 75: 124 W Garfield Ave Glendale CA 91204
    30 day value change: 68784
    rentzestimate (value): 2600
    
    
    row 76: 911 Kilmary Ln Glendale CA 91207
    30 day value change: 26418
    rentzestimate (value): 3878
    
    
    row 77: 225 Wonderview Dr Glendale CA 91202
    30 day value change: -15602
    rentzestimate (value): 5000
    
    
    row 78: 1910 Las Flores Dr Glendale CA 91207
    30 day value change: 67984
    rentzestimate (value): 3995
    
    
    row 79: 1505 Lynglen Dr Glendale CA 91206
    30 day value change: -1623
    rentzestimate (value): 4800
    
    
    row 80: 453 Salem St Glendale CA 91203
    30 day value change: 32643
    rentzestimate (value): 2450
    
    
    row 81: 1724 E Chevy Chase Dr Glendale CA 91206
    30 day value change: 17589
    rentzestimate (value): 2800
    
    
    row 82: 204 W Windsor Rd Glendale CA 91204
    30 day value change: 895
    rentzestimate (value): 2700
    
    
    row 83: 901 Penshore Terrace Glendale CA 91207
    30 day value change: 39831
    rentzestimate (value): 4500
    
    
    row 84: 420 W Elk Ave Glendale CA 91204
    30 day value change: 2237
    rentzestimate (value): 2750
    
    
    row 85: 417 Spencer St Glendale CA 91202
    30 day value change: 2680
    rentzestimate (value): 3500
    
    
    row 86: 713 S Louise St Glendale CA 91205
    30 day value change: 40424
    rentzestimate (value): 2250
    
    
    row 87: 652 Robin Glen Dr Glendale CA 91202
    not available
    30 day value change: -63033
    rentzestimate (value): 7233
    
    
    row 88: CA-2 Glendale CA
    30 day value change: 33930
    30 day value change: 6161
    30 day value change: 4863
    30 day value change: -90955
    30 day value change: 8333
    30 day value change: 1418
    30 day value change: -3188
    30 day value change: 35082
    30 day value change: -76894
    30 day value change: -35239
    30 day value change: 29638
    30 day value change: 9200
    rentzestimate (value): 3000
    rentzestimate (value): 3000
    rentzestimate (value): 2650
    rentzestimate (value): 2250
    rentzestimate (value): 2550
    rentzestimate (value): 2350
    rentzestimate (value): 2300
    rentzestimate (value): 2400
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 1850
    rentzestimate (value): 2400
    
    
    row 89: 1319 Branta Dr Glendale CA 91208
    30 day value change: 20109
    rentzestimate (value): 4500
    
    
    row 90: 1604 S Adams St Glendale CA 91205
    30 day value change: -2824
    rentzestimate (value): 2500
    
    
    row 91: CA-2 Glendale CA 91206
    30 day value change: 33930
    30 day value change: 4863
    rentzestimate (value): 3000
    rentzestimate (value): 2650
    
    
    row 92: 1219 Bruce Ave Glendale CA 91202
    30 day value change: 18818
    rentzestimate (value): 3750
    
    
    row 93: 521 Galer Pl Glendale CA 91206
    30 day value change: -4265
    rentzestimate (value): 3300
    
    
    row 94: 349 W Garfield Ave Glendale CA 91204
    30 day value change: 21820
    rentzestimate (value): 2675
    
    
    row 95: 900 S Verdugo Rd Glendale CA 91205
    30 day value change: 19887
    rentzestimate (value): 3000
    
    
    row 96: 1076 Kildonan Dr Glendale CA 91207
    30 day value change: 36111
    rentzestimate (value): 5730
    
    
    row 97: 562 Luton Dr Glendale CA 91206
    30 day value change: 2237
    rentzestimate (value): 3350
    
    
    row 98: 612 W Milford St Glendale CA 91203
    30 day value change: 3735
    rentzestimate (value): 2500
    
    
    row 99: 903 Chudleigh Ln Glendale CA 91207
    30 day value change: -14531
    rentzestimate (value): 4500
    
    
    row 100: 1901 Rimcrest Dr Glendale CA 91207
    30 day value change: 88679
    rentzestimate (value): 4553
    
    
    row 101: 428 W California Ave Glendale CA 91203
    30 day value change: -3972
    30 day value change: -5530
    30 day value change: 6053
    30 day value change: -1906
    30 day value change: 6444
    30 day value change: 7741
    30 day value change: -8586
    30 day value change: 8061
    30 day value change: 1484
    30 day value change: -5256
    30 day value change: -2459
    rentzestimate (value): 2600
    rentzestimate (value): 2400
    rentzestimate (value): 2895
    rentzestimate (value): 2550
    rentzestimate (value): 2800
    rentzestimate (value): 2750
    rentzestimate (value): 2450
    rentzestimate (value): 2990
    rentzestimate (value): 2550
    rentzestimate (value): 2500
    
    
    row 102: 1420 El Miradero Ave Glendale CA 91201
    30 day value change: 15391
    rentzestimate (value): 3795
    
    
    row 103: 1505 Wellesley Dr Glendale CA 91205
    30 day value change: 20441
    rentzestimate (value): 2600
    
    
    row 104: 951 Calle Del Pacifico Glendale CA 91208
    30 day value change: 31211
    rentzestimate (value): 4750
    
    
    row 105: 900 Kilmary Ln Glendale CA 91207
    30 day value change: -19622
    rentzestimate (value): 5400
    
    
    row 106: 1243 E Wilson Ave Glendale CA 91206
    30 day value change: 147715
    rentzestimate (value): 2700
    
    
    row 107: 516 Raleigh St Glendale CA 91205
    30 day value change: 135249
    rentzestimate (value): 2475
    
    
    row 108: 410 E Windsor Rd Glendale CA 91205
    30 day value change: 25360
    rentzestimate (value): 2500
    
    
    row 109: 1107 Glenwood Rd Glendale CA 91202
    30 day value change: 219285
    rentzestimate (value): 3500
    
    
    row 110: 2211 Bonita Dr Glendale CA 91208
    30 day value change: 5800
    rentzestimate (value): 3200
    
    
    row 111: 1620 Lamego Dr Glendale CA 91207
    30 day value change: -28193
    rentzestimate (value): 6317
    
    
    row 112: 720 Burchett St Glendale CA 91202
    30 day value change: 13777
    rentzestimate (value): 3250
    
    
    row 113: 649 Solway St Glendale CA 91206
    30 day value change: 7784
    rentzestimate (value): 3325
    
    
    row 114: 901 Lorinda Dr Glendale CA 91206
    30 day value change: 26945
    rentzestimate (value): 3500
    
    
    row 115: 545 South St Glendale CA 91202
    30 day value change: 13884
    30 day value change: 11620
    30 day value change: 11911
    30 day value change: 17361
    30 day value change: 12411
    rentzestimate (value): 2450
    rentzestimate (value): 2800
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2700
    
    
    row 116: 1416 Colina Dr Glendale CA 91208
    30 day value change: -6261
    rentzestimate (value): 3867
    
    
    row 117: 410 Canyon Dr Glendale CA 91206
    30 day value change: 10473
    rentzestimate (value): 3100
    
    
    row 118: 916 Holly St Inglewood CA 90301
    30 day value change: 5161
    rentzestimate (value): 2350
    
    
    row 119: 223 Stepney St Inglewood CA 90302
    30 day value change: 27416
    rentzestimate (value): 2175
    
    
    row 120: 8716 Endsleigh Ave Inglewood CA 90305
    30 day value change: 14227
    30 day value change: 6011
    30 day value change: 18115
    30 day value change: 14325
    30 day value change: 5918
    30 day value change: 6200
    30 day value change: 16242
    30 day value change: 6127
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    
    
    row 121: 8808 Penridge Pl Inglewood CA 90305
    30 day value change: 5741
    rentzestimate (value): 2850
    
    
    row 122: 216 W 64th Pl Inglewood CA 90302
    30 day value change: 9562
    rentzestimate (value): 2950
    
    
    row 123: 3746 W 107th St Inglewood CA 90303
    30 day value change: -36780
    rentzestimate (value): 2500
    
    
    row 124: 4954 Lennox Blvd Inglewood CA 90304
    30 day value change: 13992
    rentzestimate (value): 2500
    
    
    row 125: 470 Edgewood St Inglewood CA 90302
    30 day value change: 2192
    rentzestimate (value): 2800
    
    
    row 126: 1 E Regent St Inglewood CA 90301
    30 day value change: 8157
    30 day value change: 1991
    not available
    rentzestimate (value): 2550
    
    
    row 127: 10707 Felton Ave Inglewood CA 90304
    30 day value change: 12956
    rentzestimate (value): 2900
    
    
    row 128: 2523 W 80th St Inglewood CA 90305
    30 day value change: -2068
    rentzestimate (value): 2975
    
    
    row 129: 3428 W 111th St Inglewood CA 90303
    30 day value change: 15045
    rentzestimate (value): 2200
    
    
    row 130: 525 Hargrave St Inglewood CA 90302
    30 day value change: -3892
    rentzestimate (value): 2500
    
    
    row 131: 309 W 64th Pl Inglewood CA 90302
    30 day value change: 9828
    rentzestimate (value): 3000
    
    
    row 132: 3012 W 83rd St Inglewood CA 90305
    30 day value change: 17973
    rentzestimate (value): 2900
    
    
    row 133: 3211 W 81st St Inglewood CA 90305
    30 day value change: 5486
    rentzestimate (value): 2895
    
    
    row 134: 8915 S 6th Ave Inglewood CA 90305
    30 day value change: 8415
    rentzestimate (value): 2900
    
    
    row 135: 3206 W 82nd St Inglewood CA 90305
    30 day value change: 4218
    rentzestimate (value): 2750
    
    
    row 136: 5 Pine Ct Inglewood CA 90302
    30 day value change: 15048
    rentzestimate (value): 2800
    
    
    row 137: 209 E Fairview Blvd Inglewood CA 90302
    30 day value change: 15342
    rentzestimate (value): 2950
    
    
    row 138: 211 E 64th Pl Inglewood CA 90302
    30 day value change: 13260
    rentzestimate (value): 2995
    
    
    row 139: 3517 W 108th St Inglewood CA 90303
    30 day value change: -66818
    rentzestimate (value): 2350
    
    
    row 140: 3609 Kensley Dr Inglewood CA 90305
    30 day value change: 6367
    rentzestimate (value): 2700
    
    
    row 141: 715 Walnut St Inglewood CA 90301
    30 day value change: -207005
    rentzestimate (value): 2500
    
    
    row 142: 3729 W 110th St Inglewood CA 90303
    30 day value change: 30065
    rentzestimate (value): 2400
    
    
    row 143: 10509 S 6th Ave Inglewood CA 90303
    30 day value change: 4855
    rentzestimate (value): 3000
    
    
    row 144: 10703 8th Ave Inglewood CA 90303
    30 day value change: 13342
    rentzestimate (value): 3000
    
    
    row 145: 235 W Queen St Inglewood CA 90301
    30 day value change: 117167
    rentzestimate (value): 3000
    
    
    row 146: 3408 W 85th St Inglewood CA 90305
    30 day value change: -1322
    rentzestimate (value): 2950
    
    
    row 147: 5350 W 119th St Inglewood CA 90304
    30 day value change: 7672
    rentzestimate (value): 3200
    
    
    row 148: 3518 W 118th St Inglewood CA 90303
    30 day value change: -2125
    rentzestimate (value): 3000
    
    
    row 149: 911 Larch St Inglewood CA 90301
    30 day value change: 14671
    rentzestimate (value): 2400
    
    
    row 150: 112 N Eucalyptus Ave Inglewood CA 90301
    30 day value change: 13404
    rentzestimate (value): 2500
    
    
    row 151: 632 E Regent St Inglewood CA 90301
    30 day value change: 29804
    rentzestimate (value): 2850
    
    
    row 152: 3005 W 82nd St Inglewood CA 90305
    30 day value change: 4487
    rentzestimate (value): 2600
    
    
    row 153: 9718 S 8th Ave Inglewood CA 90305
    30 day value change: 9237
    rentzestimate (value): 2700
    
    
    row 154: 133 E Hazel St Inglewood CA 90302
    30 day value change: 23335
    rentzestimate (value): 2900
    
    
    row 155: 9316 S 3rd Ave Inglewood CA 90305
    30 day value change: 6026
    rentzestimate (value): 2795
    
    
    row 156: 10705 Buford Ave Inglewood CA 90304
    30 day value change: -5236
    rentzestimate (value): 2495
    
    
    row 157: 8808 S 11th Ave Inglewood CA 90305
    30 day value change: 290
    rentzestimate (value): 2950
    
    
    row 158: 837 Glenway Dr Inglewood CA 90302
    30 day value change: 72436
    rentzestimate (value): 2795
    
    
    row 159: 9101 S 4th Ave Inglewood CA 90305
    30 day value change: -2665
    rentzestimate (value): 2600
    
    
    row 160: 615 Manchester Dr Inglewood CA 90301
    30 day value change: 23178
    rentzestimate (value): 2750
    
    
    row 161: 5310 W 64th St Inglewood CA 90302
    30 day value change: 8941
    rentzestimate (value): 3900
    
    
    row 162: 9306 S 3rd Ave Inglewood CA 90305
    30 day value change: 3832
    rentzestimate (value): 2650
    
    
    row 163: 10609 S Freeman Ave Inglewood CA 90304
    30 day value change: -1669
    rentzestimate (value): 2500
    
    
    row 164: 320 W Regent St Inglewood CA 90301
    30 day value change: 26667
    rentzestimate (value): 2300
    
    
    row 165: 923 E Hyde Park Blvd Inglewood CA 90302
    30 day value change: 8799
    rentzestimate (value): 2500
    
    
    row 166: 11148 Lemoli Ave S Inglewood CA 90303
    30 day value change: -6209
    rentzestimate (value): 2800
    
    
    row 167: 9829 S 7th Ave Inglewood CA 90305
    30 day value change: 3342
    rentzestimate (value): 2700
    
    
    row 168: 3008 Glenridge Ave Alhambra CA 91801
    30 day value change: 24247
    rentzestimate (value): 2950
    
    
    row 169: 2240 Hitchcock Dr Alhambra CA 91803
    30 day value change: 11665
    rentzestimate (value): 2500
    
    
    row 170: 1801 S 4th St Alhambra CA 91803
    30 day value change: 8162
    rentzestimate (value): 2900
    
    
    row 171: 777 E Valley Blvd Alhambra CA 91801
    30 day value change: 5132
    30 day value change: -1292
    30 day value change: 2950
    30 day value change: 7882
    30 day value change: 23817
    30 day value change: 711
    30 day value change: 4941
    30 day value change: 3763
    30 day value change: 3846
    30 day value change: 17471
    30 day value change: 19893
    30 day value change: 5515
    30 day value change: 5786
    30 day value change: 8379
    30 day value change: 4484
    30 day value change: 6365
    30 day value change: 1329
    30 day value change: 6317
    30 day value change: 5564
    30 day value change: 6765
    30 day value change: 7619
    30 day value change: 4642
    30 day value change: 6681
    30 day value change: 7759
    30 day value change: 8090
    rentzestimate (value): 2250
    rentzestimate (value): 2200
    rentzestimate (value): 2050
    rentzestimate (value): 2250
    rentzestimate (value): 2375
    rentzestimate (value): 2250
    rentzestimate (value): 2300
    rentzestimate (value): 2400
    rentzestimate (value): 2350
    rentzestimate (value): 2500
    rentzestimate (value): 2350
    rentzestimate (value): 2295
    rentzestimate (value): 2250
    rentzestimate (value): 2250
    rentzestimate (value): 2270
    rentzestimate (value): 2400
    rentzestimate (value): 2395
    rentzestimate (value): 2260
    rentzestimate (value): 2500
    rentzestimate (value): 2250
    rentzestimate (value): 2295
    rentzestimate (value): 2250
    rentzestimate (value): 2250
    rentzestimate (value): 2230
    rentzestimate (value): 2400
    
    
    row 172: 415 Winthrop Dr Alhambra CA 91803
    30 day value change: 14124
    rentzestimate (value): 2700
    
    
    row 173: 428 W Main St Alhambra CA 91801
    not available
    30 day value change: 2410
    30 day value change: 17193
    30 day value change: 8206
    30 day value change: 9182
    30 day value change: 8317
    30 day value change: 11981
    30 day value change: 4257
    30 day value change: 3870
    30 day value change: 6428
    30 day value change: 18146
    30 day value change: 6166
    30 day value change: 5905
    30 day value change: 9428
    30 day value change: 11757
    30 day value change: 6331
    30 day value change: 6618
    30 day value change: 344
    30 day value change: 11111
    30 day value change: 13930
    30 day value change: 6744
    30 day value change: 8040
    30 day value change: 3900
    30 day value change: 6117
    30 day value change: 6120
    rentzestimate (value): 2500
    rentzestimate (value): 2975
    rentzestimate (value): 2600
    rentzestimate (value): 3000
    rentzestimate (value): 2500
    rentzestimate (value): 3000
    rentzestimate (value): 2500
    rentzestimate (value): 2950
    rentzestimate (value): 2950
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2495
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2700
    rentzestimate (value): 2900
    rentzestimate (value): 2700
    rentzestimate (value): 2695
    rentzestimate (value): 2750
    rentzestimate (value): 2500
    rentzestimate (value): 2950
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    
    
    row 174: 1600 Date Ave Alhambra CA 91803
    30 day value change: 20495
    rentzestimate (value): 2700
    
    
    row 175: 1124 N Story Pl Alhambra CA 91801
    30 day value change: -11438
    rentzestimate (value): 3100
    
    
    row 176: 2814 Poplar Blvd Alhambra CA 91803
    30 day value change: 11200
    rentzestimate (value): 2500
    
    
    row 177: 3005 Glenaven Ave Alhambra CA 91803
    30 day value change: 5071
    rentzestimate (value): 2750
    
    
    row 178: 2201 W Commonwealth Ave Alhambra CA 91803
    30 day value change: 18217
    rentzestimate (value): 2950
    
    
    row 179: 513 N El Molino St Alhambra CA 91801
    30 day value change: 11906
    rentzestimate (value): 3100
    
    
    row 180: 1121 N Monterey St Alhambra CA 91801
    30 day value change: 93181
    rentzestimate (value): 5194
    
    
    row 181: 1423 S Almansor St Alhambra CA 91801
    30 day value change: 19513
    rentzestimate (value): 2225
    
    
    row 182: 105 E Beacon St Alhambra CA 91801
    30 day value change: 29096
    30 day value change: 12610
    30 day value change: 32043
    30 day value change: 37082
    rentzestimate (value): 2500
    rentzestimate (value): 2450
    rentzestimate (value): 2400
    rentzestimate (value): 2500
    
    
    row 183: 412 S 2nd St Alhambra CA 91801
    30 day value change: 6850
    rentzestimate (value): 3500
    
    
    row 184: 529 E Mission Rd Alhambra CA 91801
    30 day value change: 8720
    30 day value change: 8694
    30 day value change: 14159
    30 day value change: -2197
    rentzestimate (value): 2500
    rentzestimate (value): 2400
    rentzestimate (value): 2500
    rentzestimate (value): 2460
    
    
    row 185: 1600 S Campbell Ave Alhambra CA 91803
    30 day value change: 19885
    rentzestimate (value): 2800
    
    
    row 186: 612 N Atlantic Blvd Alhambra CA 91801
    30 day value change: 11585
    rentzestimate (value): 2500
    
    
    row 187: 2920 Concord Ave Alhambra CA 91803
    30 day value change: 10146
    rentzestimate (value): 2395
    
    
    row 188: 210 Hampden Terrace Alhambra CA 91801
    30 day value change: 28826
    rentzestimate (value): 2600
    
    
    row 189: 1711 La Golondrina Ave Alhambra CA 91803
    30 day value change: 5471
    rentzestimate (value): 2800
    
    
    row 190: 1432 S Chapel Ave Alhambra CA 91801
    30 day value change: 24481
    rentzestimate (value): 2500
    
    
    row 191: 700 N Marguerita Ave Alhambra CA 91801
    30 day value change: 34358
    rentzestimate (value): 3200
    
    
    row 192: 219 E San Marino Ave Alhambra CA 91801
    30 day value change: 19867
    rentzestimate (value): 2900
    
    
    row 193: 1224 Benito Ave Alhambra CA 91803
    30 day value change: 18240
    rentzestimate (value): 2395
    
    
    row 194: 1705 S Vega St Alhambra CA 91801
    30 day value change: 21147
    rentzestimate (value): 2495
    
    
    row 195: 337 N Story Pl Alhambra CA 91801
    30 day value change: 74928
    rentzestimate (value): 3694
    
    
    row 196: 1002 E Beacon St Alhambra CA 91801
    30 day value change: 7352
    rentzestimate (value): 2150
    
    
    row 197: 1723 S Raymond Ave Alhambra CA 91803
    30 day value change: 10295
    rentzestimate (value): 2500
    
    
    row 198: 2012 S Monterey St Alhambra CA 91801
    30 day value change: 25071
    rentzestimate (value): 2800
    
    
    row 199: 1517 S Marengo Ave Alhambra CA 91803
    30 day value change: 14124
    rentzestimate (value): 2500
    
    
    row 200: 1-3 Halsted Cir Alhambra CA 91801
    30 day value change: 14785
    30 day value change: 9674
    rentzestimate (value): 2895
    rentzestimate (value): 3000
    
    
    row 201: 1138 Geranio Dr Alhambra CA 91801
    30 day value change: 13122
    rentzestimate (value): 2500
    
    
    row 202: 423 N Garfield Ave Alhambra CA 91801
    30 day value change: 32664
    rentzestimate (value): 2395
    
    
    row 203: 1805 S Sierra Vista Ave Alhambra CA 91801
    30 day value change: 12660
    rentzestimate (value): 2600
    
    
    row 204: 617 N Dos Robles Pl Alhambra CA 91801
    30 day value change: -250
    rentzestimate (value): 2600
    
    
    row 205: 14 S Chapel Ave Alhambra CA 91801
    30 day value change: 2670
    30 day value change: 5539
    rentzestimate (value): 2100
    rentzestimate (value): 2399
    
    
    row 206: 113 N Almansor St Alhambra CA 91801
    30 day value change: 6826
    30 day value change: 8506
    30 day value change: 13098
    30 day value change: 6762
    30 day value change: 9753
    30 day value change: 10944
    30 day value change: 20400
    30 day value change: 61508
    30 day value change: 6822
    30 day value change: 9655
    rentzestimate (value): 2600
    rentzestimate (value): 2700
    rentzestimate (value): 2600
    rentzestimate (value): 2500
    rentzestimate (value): 2600
    rentzestimate (value): 2650
    rentzestimate (value): 2600
    rentzestimate (value): 2690
    rentzestimate (value): 2700
    rentzestimate (value): 2600
    
    
    row 207: 1837 S 4th St Alhambra CA 91803
    30 day value change: 8827
    rentzestimate (value): 2840
    
    
    row 208: 1125 S New Ave Alhambra CA 91801
    30 day value change: 7146
    rentzestimate (value): 2500
    
    
    row 209: 1828 S 2nd St Alhambra CA 91801
    30 day value change: 24353
    rentzestimate (value): 2500
    
    
    row 210: 301 Orange Grove Ave Alhambra CA 91803
    30 day value change: 26447
    rentzestimate (value): 3600
    
    
    row 211: 1416 Front St Alhambra CA 91803
    30 day value change: 9440
    30 day value change: 8399
    rentzestimate (value): 2650
    rentzestimate (value): 3000
    
    
    row 212: 415 E Hellman Ave Alhambra CA 91801
    30 day value change: 18900
    rentzestimate (value): 2750
    
    
    row 213: 3009 Midwick Dr Alhambra CA 91803
    30 day value change: 6539
    rentzestimate (value): 2700
    
    
    row 214: 1412 S Olive Ave Alhambra CA 91803
    30 day value change: 28718
    rentzestimate (value): 2500
    
    
    row 215: 1105 Geranio Dr Alhambra CA 91801
    30 day value change: 21357
    rentzestimate (value): 2500
    
    
    row 216: 319 N Palm Ave Alhambra CA 91801
    30 day value change: 53986
    rentzestimate (value): 2500
    
    
    row 217: 1681 Acacia St Alhambra CA 91801
    30 day value change: 6344
    30 day value change: 7085
    30 day value change: 7995
    30 day value change: 8000
    30 day value change: 7997
    rentzestimate (value): 3295
    rentzestimate (value): 3200
    rentzestimate (value): 3300
    rentzestimate (value): 3300
    rentzestimate (value): 3300
    
    
    row 218: 817 Cherry Ave Long Beach CA 90813
    30 day value change: 115180
    rentzestimate (value): 2350
    
    
    row 219: 2900 E 7th St Long Beach CA 90804
    30 day value change: 37230
    rentzestimate (value): 3000
    
    
    row 220: 625 Coronado Ave Long Beach CA 90814
    30 day value change: 17570
    rentzestimate (value): 2300
    
    
    row 221: 2435 Pine Ave Long Beach CA 90806
    30 day value change: -5608
    rentzestimate (value): 2500
    
    
    row 222: 646 Nebraska Ave Long Beach CA 90802
    30 day value change: 3369
    30 day value change: 16322
    30 day value change: 3530
    30 day value change: 3394
    30 day value change: 3482
    30 day value change: 3359
    30 day value change: 3276
    30 day value change: 3459
    30 day value change: 2972
    30 day value change: 4078
    30 day value change: 4322
    rentzestimate (value): 2000
    rentzestimate (value): 2095
    rentzestimate (value): 1895
    rentzestimate (value): 2000
    rentzestimate (value): 2000
    rentzestimate (value): 1900
    rentzestimate (value): 1995
    rentzestimate (value): 2000
    rentzestimate (value): 1975
    rentzestimate (value): 2100
    rentzestimate (value): 2295
    
    
    row 223: 2543 Fashion Ave Long Beach CA 90812
    30 day value change: 12768
    rentzestimate (value): 2600
    
    
    row 224: E Rd Long Beach CA 90810
    30 day value change: 9498
    30 day value change: 4521
    not available
    not available
    30 day value change: 2527
    30 day value change: 12175
    30 day value change: 5602
    30 day value change: 25371
    30 day value change: 8847
    30 day value change: 5794
    30 day value change: 10889
    30 day value change: 1835
    30 day value change: 1545
    30 day value change: 6955
    30 day value change: 15374
    30 day value change: 4698
    30 day value change: 11088
    30 day value change: 3310
    30 day value change: -2962
    30 day value change: 2149
    30 day value change: 4739
    30 day value change: 15527
    30 day value change: 5202
    30 day value change: -16723
    30 day value change: -14796
    rentzestimate (value): 2400
    rentzestimate (value): 2395
    rentzestimate (value): 2300
    rentzestimate (value): 2400
    rentzestimate (value): 1995
    rentzestimate (value): 2250
    rentzestimate (value): 2200
    rentzestimate (value): 2300
    rentzestimate (value): 2200
    rentzestimate (value): 1980
    rentzestimate (value): 2600
    rentzestimate (value): 2290
    rentzestimate (value): 2100
    rentzestimate (value): 2395
    rentzestimate (value): 2700
    rentzestimate (value): 2300
    rentzestimate (value): 2600
    rentzestimate (value): 2250
    rentzestimate (value): 2275
    rentzestimate (value): 2500
    rentzestimate (value): 2400
    rentzestimate (value): 2250
    rentzestimate (value): 2600
    
    
    row 225: 3401 E First St Long Beach CA 90803
    30 day value change: -1690
    30 day value change: 5628
    30 day value change: 955
    30 day value change: 963
    30 day value change: 4583
    30 day value change: 950
    rentzestimate (value): 2750
    rentzestimate (value): 2750
    rentzestimate (value): 2550
    rentzestimate (value): 2700
    rentzestimate (value): 2799
    rentzestimate (value): 2700
    
    
    row 226: 2371 Magnolia Ave Long Beach CA 90806
    30 day value change: 29326
    rentzestimate (value): 2200
    
    
    row 227: 422 E 14th St Long Beach CA 90813
    30 day value change: 1810
    rentzestimate (value): 2450
    
    
    row 228: 2534 Adriatic Ave Long Beach CA 90810
    30 day value change: 17219
    rentzestimate (value): 2150
    
    
    row 229: 1936 Maine Ave Long Beach CA 90806
    30 day value change: 11582
    rentzestimate (value): 2400
    
    
    row 230: 1810 W Wilma Pl Long Beach CA 90810
    30 day value change: 27123
    rentzestimate (value): 2500
    
    
    row 231: 1 Junipero Ave Long Beach CA 90803
    30 day value change: 17767
    30 day value change: 6074
    rentzestimate (value): 1650
    rentzestimate (value): 2500
    
    
    row 232: 500 Orange Ave Long Beach CA 90802
    not available
    30 day value change: 2603
    30 day value change: 8483
    not available
    not available
    30 day value change: 8442
    not available
    not available
    not available
    not available
    not available
    30 day value change: 16220
    not available
    30 day value change: 8442
    rentzestimate (value): 1250
    rentzestimate (value): 1250
    rentzestimate (value): 1250
    rentzestimate (value): 1250
    rentzestimate (value): 1250
    rentzestimate (value): 1250
    rentzestimate (value): 1250
    rentzestimate (value): 1250
    rentzestimate (value): 1250
    rentzestimate (value): 2495
    
    
    row 233: 855 Lime Ave Long Beach CA 90813
    30 day value change: 20020
    rentzestimate (value): 2500
    
    
    row 234: 2680 Cedar Ave Long Beach CA 90806
    30 day value change: -262
    rentzestimate (value): 2600
    
    
    row 235: 265 Loma Ave Long Beach CA 90803
    30 day value change: 24260
    rentzestimate (value): 2300
    
    
    row 236: 374 Redondo Ave Long Beach CA 90814
    30 day value change: -8164
    rentzestimate (value): 2600
    
    
    row 237: 508 Cherry Ave Long Beach CA 90802
    30 day value change: 10560
    rentzestimate (value): 2350
    
    
    row 238: 3211 E Wilton St Long Beach CA 90804
    30 day value change: -21733
    rentzestimate (value): 2250
    
    
    row 239: 2625 E Ocean Blvd Long Beach CA 90803
    30 day value change: -58633
    rentzestimate (value): 5800
    
    
    row 240: 1925 San Francisco Ave Long Beach CA 90806
    30 day value change: 10126
    rentzestimate (value): 2700
    
    
    row 241: 437 Zona Ct Long Beach CA 90802
    30 day value change: 4902
    rentzestimate (value): 2400
    
    
    row 242: 2844 E 3rd St Long Beach CA 90814
    30 day value change: 7565
    30 day value change: 4932
    30 day value change: 4475
    30 day value change: 4620
    30 day value change: 4671
    30 day value change: 7270
    30 day value change: 4914
    30 day value change: 4914
    30 day value change: 4914
    30 day value change: 4571
    30 day value change: 4919
    30 day value change: 6656
    30 day value change: 1811
    30 day value change: 4914
    30 day value change: 6585
    30 day value change: 7265
    30 day value change: 2748
    30 day value change: 4914
    30 day value change: -7805
    30 day value change: 4632
    30 day value change: 3409
    30 day value change: 7565
    30 day value change: 5574
    30 day value change: 3336
    30 day value change: 4685
    rentzestimate (value): 2100
    rentzestimate (value): 1800
    rentzestimate (value): 2250
    rentzestimate (value): 2100
    rentzestimate (value): 1990
    rentzestimate (value): 2150
    rentzestimate (value): 1800
    rentzestimate (value): 1800
    rentzestimate (value): 1980
    rentzestimate (value): 2000
    rentzestimate (value): 2000
    rentzestimate (value): 2200
    rentzestimate (value): 2600
    rentzestimate (value): 1850
    rentzestimate (value): 2000
    rentzestimate (value): 2150
    rentzestimate (value): 2150
    rentzestimate (value): 1995
    rentzestimate (value): 2300
    rentzestimate (value): 1800
    rentzestimate (value): 2000
    rentzestimate (value): 2000
    rentzestimate (value): 2300
    rentzestimate (value): 2200
    rentzestimate (value): 2095
    
    
    row 243: 1 Junipero Ave Long Beach CA 90803
    30 day value change: 17767
    30 day value change: 6074
    rentzestimate (value): 1650
    rentzestimate (value): 2500
    
    
    row 244: 1626 Obispo Ave Long Beach CA 90804
    30 day value change: 4893
    30 day value change: 7177
    rentzestimate (value): 1950
    rentzestimate (value): 2200
    
    
    row 245: 3041 Cedar Ave Long Beach CA 90806
    30 day value change: 6127
    rentzestimate (value): 2526
    
    
    row 246: 930 E Dayman St Long Beach CA 90806
    30 day value change: 982
    rentzestimate (value): 2300
    
    
    row 247: 3116 E 15th St Long Beach CA 90804
    30 day value change: 8637
    rentzestimate (value): 2800
    
    
    row 248: 2014 Lewis Ave Long Beach CA 90806
    30 day value change: -2643
    rentzestimate (value): 2100
    
    
    row 249: 718 N Loma Vista Dr Long Beach CA 90813
    30 day value change: 15241
    rentzestimate (value): 2250
    
    
    row 250: 1341 E Wesley Dr Long Beach CA 90806
    30 day value change: -292
    rentzestimate (value): 2350
    
    
    row 251: 1084 E 19th St Long Beach CA 90806
    30 day value change: 823
    rentzestimate (value): 2300
    
    
    row 252: 3027 Pacific Avenue Long Beach CA 90806
    30 day value change: 11137
    rentzestimate (value): 2400
    
    
    row 253: 2756 Maine Ave Long Beach CA 90806
    30 day value change: 10369
    rentzestimate (value): 2800
    
    
    row 254: 372 Temple Ave Long Beach CA 90814
    30 day value change: 18066
    rentzestimate (value): 2845
    
    
    row 255: 110 245 Pine Ave Long Beach
    not available
    30 day value change: 2137
    30 day value change: -160394
    not available
    30 day value change: 2250
    rentzestimate (value): 3450
    rentzestimate (value): 20441
    rentzestimate (value): 1500
    rentzestimate (value): 950
    
    
    row 256: 2828 E 10th St Long Beach CA 90804
    30 day value change: 1100
    rentzestimate (value): 2400
    
    
    row 257: 628 Daisy Ave Long Beach CA 90802
    30 day value change: 6017
    30 day value change: 14225
    30 day value change: 1836
    30 day value change: 2559
    30 day value change: 11407
    30 day value change: 14291
    30 day value change: 15717
    30 day value change: 10175
    30 day value change: 24716
    30 day value change: 5580
    30 day value change: 3383
    30 day value change: 5973
    30 day value change: 2099
    30 day value change: 4348
    30 day value change: 3758
    30 day value change: 7592
    30 day value change: 3808
    30 day value change: 9819
    30 day value change: 11856
    30 day value change: 1929
    30 day value change: 15385
    30 day value change: -9356
    30 day value change: 15102
    30 day value change: 15829
    30 day value change: 4213
    rentzestimate (value): 2200
    rentzestimate (value): 2000
    rentzestimate (value): 1600
    rentzestimate (value): 1600
    rentzestimate (value): 2100
    rentzestimate (value): 2100
    rentzestimate (value): 2000
    rentzestimate (value): 2100
    rentzestimate (value): 2000
    rentzestimate (value): 2150
    rentzestimate (value): 1600
    rentzestimate (value): 2100
    rentzestimate (value): 1599
    rentzestimate (value): 1690
    rentzestimate (value): 1600
    rentzestimate (value): 1975
    rentzestimate (value): 1599
    rentzestimate (value): 1950
    rentzestimate (value): 1995
    rentzestimate (value): 1695
    rentzestimate (value): 2000
    rentzestimate (value): 1600
    rentzestimate (value): 2100
    rentzestimate (value): 2000
    rentzestimate (value): 1975
    
    
    row 258: 2143 Pasadena Ave Long Beach CA 90806
    30 day value change: -1786
    rentzestimate (value): 2400
    
    
    row 259: 1139 E Ocean Blvd Long Beach CA 90802
    30 day value change: 3471
    30 day value change: -7602
    30 day value change: 6008
    30 day value change: 5827
    30 day value change: -10696
    30 day value change: 8589
    30 day value change: 15584
    30 day value change: 8633
    30 day value change: 3479
    30 day value change: 26444
    30 day value change: 1652
    30 day value change: 6722
    30 day value change: 1891
    30 day value change: 2199
    30 day value change: 13487
    30 day value change: 544
    30 day value change: -12178
    30 day value change: 2047
    30 day value change: 7464
    30 day value change: 1833
    30 day value change: 1908
    30 day value change: 2121
    30 day value change: 6622
    30 day value change: 9011
    30 day value change: -4971
    rentzestimate (value): 2290
    rentzestimate (value): 2500
    rentzestimate (value): 2195
    rentzestimate (value): 2495
    rentzestimate (value): 2395
    rentzestimate (value): 2200
    rentzestimate (value): 2195
    rentzestimate (value): 2300
    rentzestimate (value): 2500
    rentzestimate (value): 4752
    rentzestimate (value): 1795
    rentzestimate (value): 2445
    rentzestimate (value): 2105
    rentzestimate (value): 2100
    rentzestimate (value): 2200
    rentzestimate (value): 2400
    rentzestimate (value): 2400
    rentzestimate (value): 1850
    rentzestimate (value): 2345
    rentzestimate (value): 2100
    rentzestimate (value): 2100
    rentzestimate (value): 2100
    rentzestimate (value): 2400
    rentzestimate (value): 2300
    rentzestimate (value): 2400
    
    
    row 260: 1 Junipero Ave Long Beach CA 90803
    30 day value change: 17767
    30 day value change: 6074
    rentzestimate (value): 1650
    rentzestimate (value): 2500
    
    
    row 261: 1099 St Louis Ave Long Beach CA 90804
    30 day value change: -10974
    rentzestimate (value): 1995
    
    
    row 262: 2370 Fashion Ave Long Beach CA 90810
    30 day value change: 2113
    rentzestimate (value): 2250
    
    
    row 263: 1935a Golden Ave Long Beach CA 90806
    30 day value change: 9272
    rentzestimate (value): 2300
    
    
    row 264: 2676 San Francisco Ave Long Beach CA 90806
    30 day value change: 2838
    rentzestimate (value): 2650
    
    
    row 265: 1 Junipero Ave Long Beach CA 90803
    30 day value change: 17767
    30 day value change: 6074
    rentzestimate (value): 1650
    rentzestimate (value): 2500
    
    
    row 266: 905 Atlantic Ave Long Beach CA 90813
    30 day value change: 4491
    rentzestimate (value): 1800
    
    
    row 267: 1077 Gaviota Ave Long Beach CA 90813
    30 day value change: 2187
    rentzestimate (value): 2100
    
    
    row 268: 739 Maine Ave Long Beach CA 90813
    30 day value change: 42831
    rentzestimate (value): 2300
    
    
    row 269: 1436B Cherry Ave Long Beach CA 90813
    30 day value change: 28224
    rentzestimate (value): 1795
    
    
    row 270: E Rd Long Beach CA 90810
    30 day value change: 9498
    30 day value change: 4521
    not available
    not available
    not available
    not available
    30 day value change: 2527
    30 day value change: 12175
    30 day value change: -2962
    30 day value change: 1545
    30 day value change: 25371
    30 day value change: 3310
    30 day value change: 7536
    30 day value change: 4695
    30 day value change: 5602
    30 day value change: -5226
    30 day value change: 3167
    30 day value change: 1316
    30 day value change: -2922
    30 day value change: 2963
    30 day value change: 3404
    30 day value change: 9229
    30 day value change: 8847
    30 day value change: 5794
    30 day value change: 2149
    rentzestimate (value): 2400
    rentzestimate (value): 2395
    rentzestimate (value): 1250
    rentzestimate (value): 2300
    rentzestimate (value): 2400
    rentzestimate (value): 2600
    rentzestimate (value): 2600
    rentzestimate (value): 2250
    rentzestimate (value): 2300
    rentzestimate (value): 2350
    rentzestimate (value): 2400
    rentzestimate (value): 1995
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2500
    rentzestimate (value): 2200
    rentzestimate (value): 2250
    rentzestimate (value): 2500
    rentzestimate (value): 2300
    rentzestimate (value): 2200
    rentzestimate (value): 2300
    rentzestimate (value): 2250
    
    
    row 271: 1865 Lewis Ave Long Beach CA 90806
    30 day value change: -215
    rentzestimate (value): 2750
    
    
    row 272: 416 Maine Ave Long Beach CA 90802
    30 day value change: 2085
    30 day value change: 6550
    rentzestimate (value): 2100
    rentzestimate (value): 2300
    
    
    row 273: 2640 Santa Fe Ave Long Beach CA 90810
    30 day value change: 6186
    rentzestimate (value): 2460
    
    
    row 274: 152 N Park View St Los Angeles CA 90026
    30 day value change: 38850
    rentzestimate (value): 2800
    
    
    row 275: 2518 Berkeley Ave Los Angeles CA 90026
    30 day value change: 13363
    rentzestimate (value): 2500
    
    
    row 276: 1890 Silver Lake Blvd Los Angeles CA 90026
    30 day value change: -32880
    rentzestimate (value): 3400
    
    
    row 277: 2225 Montana St Los Angeles CA 90026
    30 day value change: -32732
    rentzestimate (value): 2600
    
    
    row 278: 2012 Valentine St Los Angeles CA 90026
    30 day value change: -1341
    rentzestimate (value): 2500
    
    
    row 279: 145 S Dacotah St Los Angeles CA 90063
    30 day value change: 4845
    rentzestimate (value): 2250
    
    
    row 280: 2822 Cincinnati St Los Angeles CA 90033
    30 day value change: 2394
    rentzestimate (value): 2400
    
    
    row 281: 212 S Chicago St Los Angeles CA 90033
    30 day value change: 1599
    rentzestimate (value): 2300
    
    
    row 282: 415 N Soto St Los Angeles CA 90033
    30 day value change: 4794
    rentzestimate (value): 2250
    
    
    row 283: 1421 Carroll Ave Los Angeles CA 90026
    30 day value change: 31018
    rentzestimate (value): 2600
    
    
    row 284: 2434 Johnston St Los Angeles CA 90031
    30 day value change: 7900
    rentzestimate (value): 2500
    
    
    row 285: 1504 E 20th St Los Angeles CA 90011
    30 day value change: -15260
    rentzestimate (value): 2500
    
    
    row 286: 720 E Edgeware Rd Los Angeles CA 90026
    30 day value change: 43190
    rentzestimate (value): 2600
    
    
    row 287: 620 W 6th St Los Angeles CA 90017
    30 day value change: 3839
    rentzestimate (value): 2300
    
    
    row 288: 2007 Lake Shore Ave Los Angeles CA 90039
    30 day value change: 32804
    rentzestimate (value): 3700
    
    
    row 289: 1944 Sheridan St Los Angeles CA 90033
    30 day value change: 12272
    rentzestimate (value): 2250
    
    
    row 290: 435 S Lafayette Park Pl Los Angeles CA 90057
    30 day value change: -10538
    30 day value change: -14496
    30 day value change: -2779
    30 day value change: -761
    30 day value change: -6474
    30 day value change: 9770
    30 day value change: -5875
    30 day value change: -2863
    30 day value change: 9772
    30 day value change: -10463
    30 day value change: 9792
    30 day value change: -10235
    30 day value change: 9868
    30 day value change: 9850
    30 day value change: 3
    30 day value change: 366
    not available
    30 day value change: 366
    30 day value change: -5201
    30 day value change: -4089
    30 day value change: -101
    30 day value change: 366
    30 day value change: -2588
    30 day value change: -10852
    30 day value change: 9772
    rentzestimate (value): 2750
    rentzestimate (value): 2750
    rentzestimate (value): 2695
    rentzestimate (value): 2600
    rentzestimate (value): 2600
    rentzestimate (value): 2600
    rentzestimate (value): 2600
    rentzestimate (value): 2550
    rentzestimate (value): 2600
    rentzestimate (value): 2700
    rentzestimate (value): 2600
    rentzestimate (value): 2650
    rentzestimate (value): 2650
    rentzestimate (value): 2650
    rentzestimate (value): 2695
    rentzestimate (value): 2600
    rentzestimate (value): 2600
    rentzestimate (value): 2600
    rentzestimate (value): 2750
    rentzestimate (value): 2600
    rentzestimate (value): 2600
    rentzestimate (value): 2600
    rentzestimate (value): 2550
    rentzestimate (value): 2695
    rentzestimate (value): 2600
    
    
    row 291: 156 S Pecan St Los Angeles CA 90033
    30 day value change: 5683
    rentzestimate (value): 2400
    
    
    row 292: 2450 Marengo St Los Angeles CA 90033
    30 day value change: 30506
    rentzestimate (value): 2400
    
    
    row 293: 1719 Echo Park Ave Los Angeles CA 90026
    30 day value change: -15892
    rentzestimate (value): 2850
    
    
    row 294: 1326 Venice Blvd Los Angeles CA 90006
    30 day value change: 10089
    rentzestimate (value): 2600
    
    
    row 295: 1060 N Fickett St Los Angeles CA 90033
    30 day value change: -9978
    rentzestimate (value): 2550
    
    
    row 296: 1141 Laveta Terrace Los Angeles CA 90026
    30 day value change: 17665
    rentzestimate (value): 3542
    
    
    row 297: 3051 Oregon St Los Angeles CA 90023
    30 day value change: 10387
    rentzestimate (value): 2500
    
    
    row 298: 656 Judson St Los Angeles CA 90033
    30 day value change: -6450
    rentzestimate (value): 2450
    
    
    row 299: 1627 Cortez St Los Angeles CA 90026
    30 day value change: 18349
    rentzestimate (value): 2495
    
    
    row 300: 325 S Reno St Los Angeles CA 90057
    30 day value change: 17719
    rentzestimate (value): 3505
    
    
    row 301: 450 E 31st St Los Angeles CA 90011
    30 day value change: 44180
    rentzestimate (value): 2500
    
    
    row 302: 2900 Guirado St Los Angeles CA 90023
    30 day value change: 4839
    rentzestimate (value): 2250
    
    
    row 303: 642 S Soto St Los Angeles CA 90023
    30 day value change: 12349
    rentzestimate (value): 2395
    
    
    row 304: 1150 E 40th Pl Los Angeles CA 90011
    30 day value change: 9903
    rentzestimate (value): 2400
    
    
    row 305: 420 S Lafayette Park Pl Los Angeles CA 90057
    30 day value change: 3865
    rentzestimate (value): 1960
    
    
    row 306: 1707 S Burlington Ave Los Angeles CA 90006
    30 day value change: 35658
    rentzestimate (value): 2600
    
    
    row 307: 2512 Marathon St Los Angeles CA 90026
    30 day value change: 11198
    rentzestimate (value): 2500
    
    
    row 308: 2124 Manitou Ave Los Angeles CA 90031
    30 day value change: -6122
    rentzestimate (value): 3095
    
    
    row 309: 917 E Adams Blvd Los Angeles CA 90011
    30 day value change: 8517
    rentzestimate (value): 2400
    
    
    row 310: 2815 Reservoir St Los Angeles CA 90026
    30 day value change: -7200
    rentzestimate (value): 3200
    
    
    row 311: 2215 Park Dr Los Angeles CA 90026
    30 day value change: 73521
    rentzestimate (value): 2795
    
    
    row 312: 1148 N Cummings St Los Angeles CA 90033
    30 day value change: 7005
    rentzestimate (value): 2300
    
    
    row 313: 1034 Albany St Los Angeles CA 90015
    30 day value change: 31198
    rentzestimate (value): 2395
    
    
    row 314: 2725 Michigan Ave Los Angeles CA 90033
    30 day value change: 16195
    rentzestimate (value): 2200
    
    
    row 315: 2647 Chelsea St Los Angeles CA 90033
    30 day value change: 17426
    rentzestimate (value): 2500
    
    
    row 316: 2249 Hancock St Los Angeles CA 90031
    30 day value change: -4597
    rentzestimate (value): 2500
    
    
    row 317: 1301 N Coronado St Los Angeles CA 90026
    30 day value change: 6872
    rentzestimate (value): 3000
    
    
    row 318: 111 N Central Ave Los Angeles CA 90012
    30 day value change: 12503
    30 day value change: 878
    not available
    not available
    rentzestimate (value): 2450
    rentzestimate (value): 2800
    rentzestimate (value): 1775
    rentzestimate (value): 2450
    
    
    row 319: 435 E 32nd St Los Angeles CA 90011
    30 day value change: 7703
    rentzestimate (value): 2300
    
    
    row 320: 1701 Apex Ave Los Angeles CA 90026
    30 day value change: -13423
    rentzestimate (value): 6307
    
    
    row 321: 1408 Westerly Terrace Los Angeles CA 90026
    30 day value change: -2824
    rentzestimate (value): 3200
    
    
    row 322: 142 N Ave 25 Los Angeles CA 90031
    30 day value change: 6189
    rentzestimate (value): 2350
    
    
    row 323: 1522 W Temple St Los Angeles CA 90026
    30 day value change: 13766
    rentzestimate (value): 2500
    
    
    row 324: 1011 Coronado Terrace Los Angeles CA 90026
    30 day value change: 11252
    rentzestimate (value): 2650
    
    
    row 325: 2741 Eagle St Los Angeles CA 90033
    30 day value change: 5473
    rentzestimate (value): 2400
    
    
    row 326: 140 W Ave 30 Los Angeles CA 90031
    30 day value change: -4275
    rentzestimate (value): 2500
    
    
    row 327: 217 W 1st St Los Angeles CA 90012
    30 day value change: 6138
    rentzestimate (value): 2600
    
    
    row 328: 2407 E 2nd St Los Angeles CA 90033
    30 day value change: 2398
    rentzestimate (value): 2250
    
    
    row 329: 1844 Silverwood Terrace Los Angeles CA 90026
    30 day value change: -6311
    rentzestimate (value): 9594
    
    
    row 330: 1335 Pennsylvania Ave Los Angeles CA 90033
    30 day value change: 5201
    rentzestimate (value): 2800
    
    
    row 331: 425 N Boylston St Los Angeles CA 90012
    30 day value change: -2226
    rentzestimate (value): 2950
    
    
    row 332: W 7th St Palmdale CA 93551
    
    
    row 333: Country Club Dr Palmdale CA 93551
    30 day value change: 7513
    30 day value change: 1920
    30 day value change: 3569
    30 day value change: -290
    30 day value change: 3349
    30 day value change: 3891
    30 day value change: -2834
    30 day value change: 3584
    30 day value change: 7856
    30 day value change: 4641
    30 day value change: 3900
    30 day value change: 3403
    30 day value change: 7375
    30 day value change: 3672
    30 day value change: 7540
    30 day value change: 6670
    30 day value change: -767
    30 day value change: 5871
    30 day value change: 2988
    30 day value change: 8567
    30 day value change: 2842
    30 day value change: 3676
    30 day value change: 21587
    30 day value change: 3880
    30 day value change: 5108
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2100
    rentzestimate (value): 2200
    rentzestimate (value): 2100
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2100
    rentzestimate (value): 1850
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 1800
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2250
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2400
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2100
    rentzestimate (value): 2200
    
    
    row 335: 1750 E Ave Q14 Palmdale CA 93550
    30 day value change: 2059
    rentzestimate (value): 1450
    
    
    row 337: 143 W Ave S-14 Palmdale CA 93551
    30 day value change: -37491
    rentzestimate (value): 5241
    
    
    row 338: 820 W Avenue P Palmdale CA 93551
    not available
    30 day value change: 6944
    30 day value change: 7612
    30 day value change: 12667
    rentzestimate (value): 2400
    rentzestimate (value): 2400
    rentzestimate (value): 2300
    
    
    row 339: 2634 E Ave Q-15 Palmdale CA 93550
    30 day value change: 3444
    rentzestimate (value): 1950
    
    
    row 340: 38969 Yucca Tree St Palmdale CA 93551
    30 day value change: 2494
    rentzestimate (value): 1783
    
    
    row 341: 450 W Ave O Palmdale CA 93551
    30 day value change: 6157
    30 day value change: -60
    rentzestimate (value): 2495
    rentzestimate (value): 2200
    
    
    row 342: 37217 Weeping Branch St Palmdale CA 93550
    30 day value change: 3805
    rentzestimate (value): 2300
    
    
    row 343: 37457 Conifer Dr Palmdale CA 93550
    30 day value change: 3050
    rentzestimate (value): 1750
    
    
    row 345: 39261 10th St E Palmdale CA 93550
    30 day value change: 24439
    rentzestimate (value): 2100
    
    
    row 346: 1656 Korat Dr Palmdale CA 93551
    30 day value change: 4881
    rentzestimate (value): 2200
    
    
    row 347: 1607 Via Verde Ave Palmdale CA 93550
    30 day value change: 3884
    rentzestimate (value): 1700
    
    
    row 348: 38575 Friendly Ave Palmdale CA 93550
    30 day value change: 5734
    rentzestimate (value): 1600
    
    
    row 349: 1817 A E Ave Q Palmdale CA 93550
    30 day value change: 3679
    not available
    not available
    30 day value change: -1898
    30 day value change: 5754
    30 day value change: 4419
    30 day value change: 5051
    30 day value change: 5271
    30 day value change: 4087
    rentzestimate (value): 1750
    rentzestimate (value): 2550
    rentzestimate (value): 2195
    rentzestimate (value): 2000
    rentzestimate (value): 1850
    rentzestimate (value): 1650
    rentzestimate (value): 2000
    
    
    row 350: 1845 E Avenue Q12 Palmdale CA 93550
    30 day value change: 1902
    rentzestimate (value): 1495
    
    
    row 351: 458 E Avenue R-5 Palmdale CA 93550
    30 day value change: 3603
    rentzestimate (value): 1600
    
    
    row 352: 505 Hansa St Palmdale CA 93551
    30 day value change: -1191
    rentzestimate (value): 2300
    
    
    row 353: 37135 Tovey Ave Palmdale CA 93551
    30 day value change: 2253
    rentzestimate (value): 2400
    
    
    row 354: 36517 China Pl Palmdale CA 93551
    30 day value change: -2039
    rentzestimate (value): 3100
    
    
    row 355: 545 Spruce Ct Palmdale CA 93550
    30 day value change: 2801
    rentzestimate (value): 1650
    
    
    row 356: 340 W Avenue P Palmdale CA 93551
    30 day value change: 6137
    30 day value change: 8706
    30 day value change: 11383
    30 day value change: 5475
    30 day value change: 5766
    rentzestimate (value): 2200
    rentzestimate (value): 2100
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    
    
    row 357: 2201 E Ave Q Palmdale CA 93550
    30 day value change: 3436
    30 day value change: 5028
    30 day value change: 6146
    30 day value change: 8107
    rentzestimate (value): 2000
    rentzestimate (value): 2000
    rentzestimate (value): 1995
    rentzestimate (value): 2000
    
    
    row 358: Country Club Dr Palmdale CA 93551
    30 day value change: 7513
    30 day value change: 1920
    30 day value change: 3569
    30 day value change: -290
    30 day value change: 3349
    30 day value change: 3891
    30 day value change: -2834
    30 day value change: 3584
    30 day value change: 7856
    30 day value change: 4641
    30 day value change: 3900
    30 day value change: 3403
    30 day value change: 7375
    30 day value change: 3672
    30 day value change: 7540
    30 day value change: 6670
    30 day value change: -767
    30 day value change: 5871
    30 day value change: 2988
    30 day value change: 8567
    30 day value change: 2842
    30 day value change: 3676
    30 day value change: 21587
    30 day value change: 3880
    30 day value change: 5108
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2100
    rentzestimate (value): 2200
    rentzestimate (value): 2100
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2100
    rentzestimate (value): 1850
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 1800
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2250
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2400
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 2100
    rentzestimate (value): 2200
    
    
    row 359: 38448 Yucca Tree St Palmdale CA 93551
    30 day value change: 3842
    rentzestimate (value): 2200
    
    
    row 360: 268 E Ave P 2 Palmdale CA 93550
    30 day value change: 2502
    rentzestimate (value): 1600
    
    
    row 361: 2436 Estrella Ct Palmdale CA 93550
    30 day value change: 2838
    rentzestimate (value): 2100
    
    
    row 362: 36213 El Camino Dr Palmdale CA 93551
    30 day value change: 11147
    rentzestimate (value): 2750
    
    
    row 363: 37135 Tovey Ave Palmdale CA 93551
    30 day value change: 2253
    rentzestimate (value): 2400
    
    
    row 364: 36213 El Camino Dr Palmdale CA 93551
    30 day value change: 11147
    rentzestimate (value): 2750
    
    
    row 365: 2129 Moonlight Ct Palmdale CA 93550
    30 day value change: 3846
    rentzestimate (value): 1995
    
    
    row 366: 38618 20th St E Palmdale CA 93550
    30 day value change: 805
    rentzestimate (value): 2040
    
    
    row 367: 36213 El Camino Dr Palmdale CA 93551
    30 day value change: 11147
    rentzestimate (value): 2750
    
    
    row 368: 37135 Tovey Ave Palmdale CA 93551
    30 day value change: 2253
    rentzestimate (value): 2400
    
    
    row 369: 1834 Sweetbrier St Palmdale CA 93550
    30 day value change: 2059
    rentzestimate (value): 1550
    
    
    row 370: 241 Quail Dr Palmdale CA 93551
    30 day value change: -2208
    rentzestimate (value): 2435
    
    
    row 371: 1141 E Ave R Palmdale CA 93550
    30 day value change: 720
    30 day value change: 31283
    30 day value change: -26750
    rentzestimate (value): 1695
    rentzestimate (value): 1795
    rentzestimate (value): 1600
    
    
    row 372: 311 Bogie St Palmdale CA 93551
    30 day value change: 5816
    rentzestimate (value): 2200
    
    
    row 373: 548 W Ave Q 12 Palmdale CA 93551
    30 day value change: 7657
    rentzestimate (value): 2100
    
    
    row 374: 37414 Larchwood Dr Palmdale CA 93550
    30 day value change: 1788
    rentzestimate (value): 1850
    
    
    row 375: 2801 E Ave S Palmdale CA 93550
    30 day value change: 3294
    30 day value change: 3145
    30 day value change: 6150
    30 day value change: 1102
    rentzestimate (value): 1775
    rentzestimate (value): 2200
    rentzestimate (value): 2200
    rentzestimate (value): 1700
    
    
    row 376: 37031 Cooper Terrace Palmdale CA 93550
    30 day value change: 3633
    rentzestimate (value): 1600
    
    
    row 377: 2321 E Ave S Palmdale CA 93550
    30 day value change: 5107
    rentzestimate (value): 1699
    
    
    row 378: 37405 7th St W Palmdale CA 93551
    30 day value change: -4981
    rentzestimate (value): 2500
    
    
    row 379: 2904 E Ave R10 Palmdale CA 93550
    30 day value change: 2519
    rentzestimate (value): 1950
    
    
    row 380: 40140 Pevero Ct Palmdale CA 93551
    30 day value change: 4283
    rentzestimate (value): 2200
    
    
    row 381: 2202 E Ave R 10 Palmdale CA 93550
    30 day value change: 3549
    30 day value change: 4165
    rentzestimate (value): 2000
    rentzestimate (value): 2300
    
    
    row 382: 2231 E Ave Q Palmdale CA 93550
    30 day value change: 2152
    30 day value change: 2561
    30 day value change: 5474
    rentzestimate (value): 2000
    rentzestimate (value): 1800
    rentzestimate (value): 2000
    
    
    row 383: 2010 E Ave R Palmdale CA 93550
    30 day value change: 4277
    30 day value change: 6706
    30 day value change: 3474
    30 day value change: 5264
    rentzestimate (value): 2000
    rentzestimate (value): 1550
    rentzestimate (value): 1595
    rentzestimate (value): 1995
    
    
    row 384: 37642 Gilworth Ave Palmdale CA 93550
    30 day value change: -1244
    rentzestimate (value): 1600
    
    
    row 385: 36506 China Pl Palmdale CA 93551
    30 day value change: -2017
    rentzestimate (value): 3200
    
    
    row 386: 2208 E Ave R12 Palmdale CA 93550
    30 day value change: 2571
    rentzestimate (value): 2000
    
    
    row 387: 38409 Sphynx Dr Palmdale CA 93551
    30 day value change: 4240
    rentzestimate (value): 2295
    
    
    row 388: 37302 Sand Brook Dr Palmdale CA 93550
    30 day value change: 2481
    rentzestimate (value): 2000
    
    
    row 389: 2424 Swallow Ln Palmdale CA 93550
    30 day value change: 4249
    rentzestimate (value): 2395
    
    
    row 390: 2152 Spanish Broom Dr Palmdale CA 93550
    30 day value change: 15675
    
    
    row 391: 700 Union St Pasadena CA 91101
    30 day value change: 9761
    30 day value change: 3606
    30 day value change: 6881
    30 day value change: 4356
    30 day value change: 11617
    30 day value change: 15853
    30 day value change: 8728
    30 day value change: 26
    30 day value change: 13775
    30 day value change: -3265
    30 day value change: 20928
    30 day value change: 21293
    30 day value change: 5659
    30 day value change: 9179
    30 day value change: 20842
    30 day value change: 236
    30 day value change: 11593
    30 day value change: -5717
    30 day value change: -2679
    30 day value change: 3272
    30 day value change: 11173
    30 day value change: 18072
    30 day value change: 7346
    30 day value change: 17688
    30 day value change: 5507
    rentzestimate (value): 2850
    rentzestimate (value): 2500
    rentzestimate (value): 3200
    rentzestimate (value): 2500
    rentzestimate (value): 3603
    rentzestimate (value): 2850
    rentzestimate (value): 3200
    rentzestimate (value): 2150
    rentzestimate (value): 4633
    rentzestimate (value): 3000
    rentzestimate (value): 4453
    rentzestimate (value): 2900
    rentzestimate (value): 2900
    rentzestimate (value): 3518
    rentzestimate (value): 2650
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2200
    rentzestimate (value): 2400
    rentzestimate (value): 2700
    rentzestimate (value): 3607
    rentzestimate (value): 3200
    rentzestimate (value): 3300
    rentzestimate (value): 2950
    rentzestimate (value): 2300
    
    
    row 392: 330 Cordova St Pasadena CA 91101
    30 day value change: 24724
    30 day value change: 40616
    rentzestimate (value): 2750
    
    
    row 393: 1100 Hermosa Rd Pasadena CA 91105
    30 day value change: 16379
    rentzestimate (value): 7480
    
    
    row 394: 71 San Miguel Rd Pasadena CA 91105
    30 day value change: -66956
    rentzestimate (value): 5965
    
    
    row 395: 36 S Parkwood Ave Pasadena CA 91107
    30 day value change: 55521
    rentzestimate (value): 2600
    
    
    row 396: 625 Prospect Blvd Pasadena CA 91103
    30 day value change: 6895
    rentzestimate (value): 10390
    
    
    row 397: 1121 Heatherside Rd Pasadena CA 91105
    30 day value change: 16873
    rentzestimate (value): 3998
    
    
    row 398: 1470 E California Blvd Pasadena CA 91106
    30 day value change: -96458
    rentzestimate (value): 21912
    
    
    row 399: 1566 Mentone Ave Pasadena CA 91103
    30 day value change: 4876
    rentzestimate (value): 2750
    
    
    row 400: 1463 Forest Ave Pasadena CA 91103
    30 day value change: 7977
    rentzestimate (value): 2275
    
    
    row 401: 1300 Glen Oaks Blvd Pasadena CA 91105
    30 day value change: 54024
    rentzestimate (value): 10083
    
    
    row 402: 1929 Mill Rd South Pasadena CA 91030
    30 day value change: 24318
    rentzestimate (value): 2695
    
    
    row 403: 1455 Chamberlain Rd Pasadena CA 91103
    30 day value change: 76560
    rentzestimate (value): 7529
    
    
    row 404: 1233 Encino Dr Pasadena CA 91108
    30 day value change: -120583
    rentzestimate (value): 12154
    
    
    row 405: 178 N Madison Ave Pasadena CA 91101
    30 day value change: -10187
    rentzestimate (value): 2550
    
    
    row 406: 1432 Wayne Ave South Pasadena CA 91030
    30 day value change: 46737
    rentzestimate (value): 6227
    
    
    row 407: 484 E California Blvd Pasadena CA 91106
    30 day value change: 10677
    30 day value change: 9416
    30 day value change: -10804
    30 day value change: 11481
    30 day value change: 569
    30 day value change: 13822
    30 day value change: 2451
    30 day value change: 85
    30 day value change: 9975
    30 day value change: 2146
    30 day value change: 12809
    30 day value change: 10066
    30 day value change: 10461
    30 day value change: -13072
    30 day value change: -11558
    30 day value change: 6663
    30 day value change: 10727
    30 day value change: 12068
    30 day value change: 13751
    30 day value change: 13823
    30 day value change: 2613
    30 day value change: 15731
    30 day value change: 284
    30 day value change: 50362
    30 day value change: -616
    rentzestimate (value): 2700
    rentzestimate (value): 2695
    rentzestimate (value): 2500
    rentzestimate (value): 2750
    rentzestimate (value): 2700
    rentzestimate (value): 2800
    rentzestimate (value): 2900
    rentzestimate (value): 2600
    rentzestimate (value): 3000
    rentzestimate (value): 2800
    rentzestimate (value): 2950
    rentzestimate (value): 2500
    rentzestimate (value): 2700
    rentzestimate (value): 2400
    rentzestimate (value): 2595
    rentzestimate (value): 2500
    rentzestimate (value): 2795
    rentzestimate (value): 3000
    rentzestimate (value): 2800
    rentzestimate (value): 2700
    rentzestimate (value): 2600
    rentzestimate (value): 2695
    rentzestimate (value): 2600
    rentzestimate (value): 2500
    rentzestimate (value): 2700
    
    
    row 408: 433 S Greenwood Ave Pasadena CA 91107
    30 day value change: 2164
    rentzestimate (value): 3811
    
    
    row 409: 1408 N Holliston Ave Pasadena CA 91104
    30 day value change: 15350
    rentzestimate (value): 2450
    
    
    row 410: 1600 La Vista Pl Pasadena CA 91103
    30 day value change: -42215
    rentzestimate (value): 9534
    
    
    row 411: 1079 Marengo Ave Pasadena CA 91103
    30 day value change: 40371
    rentzestimate (value): 3400
    
    
    row 412: 270 Del Monte St Pasadena CA 91103
    30 day value change: 1006
    rentzestimate (value): 2600
    
    
    row 413: 272 S Michigan Ave Pasadena CA 91106
    30 day value change: 34473
    rentzestimate (value): 2800
    
    
    row 414: 475 Bellmore Way Pasadena CA 91103
    30 day value change: 29461
    rentzestimate (value): 7519
    
    
    row 415: 570 E Glenarm St Pasadena CA 91106
    30 day value change: 25315
    rentzestimate (value): 9587
    
    
    row 416: 1808 Las Lunas St Pasadena CA 91107
    30 day value change: 52998
    rentzestimate (value): 3200
    
    
    row 417: 538 N Holliston Ave Pasadena CA 91106
    30 day value change: 44604
    rentzestimate (value): 2500
    
    
    row 418: 312 Fairview Ave South Pasadena CA 91030
    30 day value change: 23785
    rentzestimate (value): 3411
    
    
    row 419: 124 Waverly Dr Pasadena CA 91105
    30 day value change: 40640
    rentzestimate (value): 2800
    
    
    row 420: 497 E California Blvd Pasadena CA 91106
    30 day value change: 10355
    30 day value change: 7498
    30 day value change: 3803
    30 day value change: 3805
    30 day value change: 3697
    30 day value change: 64865
    30 day value change: 7216
    30 day value change: -3929
    30 day value change: -3128
    30 day value change: 12435
    30 day value change: 7293
    30 day value change: 7241
    30 day value change: 17248
    30 day value change: -1050
    30 day value change: 3803
    30 day value change: -2902
    30 day value change: 9636
    30 day value change: -3171
    30 day value change: 7293
    30 day value change: 720
    30 day value change: 7214
    30 day value change: 3937
    30 day value change: 7214
    30 day value change: 7489
    30 day value change: 3803
    rentzestimate (value): 2700
    rentzestimate (value): 2650
    rentzestimate (value): 2450
    rentzestimate (value): 2450
    rentzestimate (value): 2500
    rentzestimate (value): 2500
    rentzestimate (value): 2675
    rentzestimate (value): 2650
    rentzestimate (value): 2500
    rentzestimate (value): 2700
    rentzestimate (value): 2650
    rentzestimate (value): 2650
    rentzestimate (value): 2500
    rentzestimate (value): 2395
    rentzestimate (value): 2450
    rentzestimate (value): 2750
    rentzestimate (value): 2550
    rentzestimate (value): 2650
    rentzestimate (value): 2650
    rentzestimate (value): 2700
    rentzestimate (value): 2650
    rentzestimate (value): 2500
    rentzestimate (value): 2650
    rentzestimate (value): 2675
    rentzestimate (value): 2450
    
    
    row 421: 387 Mira Vista Terrace Pasadena CA 91105
    30 day value change: 78922
    rentzestimate (value): 8573
    
    
    row 422: 745 S Oakland Ave Pasadena CA 91106
    30 day value change: -13038
    rentzestimate (value): 6566
    
    
    row 423: 714 N Michigan Ave Pasadena CA 91104
    30 day value change: 1498
    rentzestimate (value): 3200
    
    
    row 424: 1476 Rutherford Dr Pasadena CA 91103
    30 day value change: -72097
    rentzestimate (value): 9024
    
    
    row 425: 686 S Arroyo Blvd Pasadena CA 91105
    30 day value change: 73808
    rentzestimate (value): 8169
    
    
    row 426: 153 S Grand Oaks Ave Pasadena CA 91107
    30 day value change: 20738
    rentzestimate (value): 2350
    
    
    row 427: 1267 Sunset Ave Pasadena CA 91103
    30 day value change: 60377
    rentzestimate (value): 2300
    
    
    row 428: 718 Hermosa St South Pasadena CA 91030
    30 day value change: 41954
    rentzestimate (value): 7793
    
    
    row 429: 417 S Hudson Ave Pasadena CA 91101
    30 day value change: 4133
    rentzestimate (value): 2500
    
    
    row 430: 909 S El Molino Ave Pasadena CA 91106
    30 day value change: -45392
    rentzestimate (value): 5532
    
    
    row 431: 376 S Marengo Ave Pasadena CA 91101
    30 day value change: 2626
    rentzestimate (value): 2200
    
    
    row 432: 125 S Grand Ave Pasadena CA 91105
    not available
    30 day value change: -350186
    rentzestimate (value): 20422
    
    
    row 433: 544 Garfield Ave South Pasadena CA 91030
    30 day value change: 7738
    rentzestimate (value): 3375
    
    
    row 434: 1605 Pleasant Way Pasadena CA 91105
    30 day value change: -6222
    rentzestimate (value): 3856
    
    
    row 435: 430 Laguna Rd Pasadena CA 91105
    30 day value change: 49929
    rentzestimate (value): 9675
    
    
    row 436: 365 Atchison St Pasadena CA 91104
    30 day value change: -10239
    rentzestimate (value): 3250
    
    
    row 437: 1450 West Dr Pasadena CA 91105
    30 day value change: -41589
    30 day value change: 26649
    not available
    30 day value change: 7411
    30 day value change: 6565
    rentzestimate (value): 9519
    rentzestimate (value): 4180
    rentzestimate (value): 4262
    rentzestimate (value): 3666
    
    
    row 438: 931 N Michigan Ave Pasadena CA 91104
    30 day value change: 19044
    rentzestimate (value): 3200
    
    
    row 439: 555 Glen Ct Pasadena CA 91105
    30 day value change: 9311
    rentzestimate (value): 9836
    
    
    row 440: 1501 Locust St Pasadena CA 91106
    30 day value change: 15714
    rentzestimate (value): 2500
    
    
    row 441: 1025 N Mentor Ave Pasadena CA 91104
    30 day value change: 9392
    rentzestimate (value): 3250
    
    
    row 442: 21563 Cleardale St Santa Clarita CA 91321
    30 day value change: 10447
    rentzestimate (value): 2300
    
    
    row 443: 24001 Briardale Way Santa Clarita CA 91321
    30 day value change: 13317
    rentzestimate (value): 3500
    
    
    row 444: 26327 Emerald Dove Dr Santa Clarita CA 91355
    30 day value change: 22494
    rentzestimate (value): 2615
    
    
    row 445: 22405 Cardiff Dr Santa Clarita CA 91350
    30 day value change: 6826
    rentzestimate (value): 3200
    
    
    row 446: 26215 Paolino Pl Santa Clarita CA 91355
    30 day value change: 7106
    rentzestimate (value): 3100
    
    
    row 447: 25458 Ave Escalera Santa Clarita CA 91355
    30 day value change: 7836
    rentzestimate (value): 3200
    
    
    row 448: 23649 Newhall Ave Santa Clarita CA 91321
    30 day value change: -5967
    rentzestimate (value): 2800
    
    
    row 449: 23614 Neargate Dr Santa Clarita CA 91321
    30 day value change: 10577
    rentzestimate (value): 2995
    
    
    row 450: 24902 Avignon Dr Santa Clarita CA 91355
    30 day value change: 8253
    rentzestimate (value): 2800
    
    
    row 451: 23649 Newhall Ave Santa Clarita CA 91321
    30 day value change: -5967
    rentzestimate (value): 2800
    
    
    row 452: 22503 Los Tigres Dr Santa Clarita CA 91350
    30 day value change: 10545
    rentzestimate (value): 2600
    
    
    row 453: 23401 Westford Pl Santa Clarita CA 91354
    30 day value change: 8161
    rentzestimate (value): 3250
    
    
    row 454: 25549 Sheffield Ln Santa Clarita CA 91350
    30 day value change: 11229
    rentzestimate (value): 3000
    
    
    row 455: 26028 Tourelle Pl Santa Clarita CA 91355
    30 day value change: -540
    rentzestimate (value): 3400
    
    
    row 456: 24001 Briardale Way Santa Clarita CA 91321
    30 day value change: 13317
    rentzestimate (value): 3500
    
    
    row 457: 23402 Gaucho Ct Santa Clarita CA 91355
    30 day value change: 2392
    rentzestimate (value): 2250
    
    
    row 458: 26614 Gavilan Dr Santa Clarita CA 91350
    30 day value change: 5754
    rentzestimate (value): 2750
    
    
    row 459: 23960 Wildwood Canyon Rd Santa Clarita CA 91321
    30 day value change: 91291
    rentzestimate (value): 12000
    
    
    row 460: 26579 Bouquet Canyon Rd Santa Clarita CA 91350
    30 day value change: 10411
    rentzestimate (value): 3400
    
    
    row 461: 23463 Cherry St Santa Clarita CA 91321
    30 day value change: 10336
    rentzestimate (value): 2400
    
    
    row 462: 23306 Maple St Santa Clarita CA 91321
    30 day value change: 12172
    rentzestimate (value): 5500
    
    
    row 463: 25565 Vía Paladar Santa Clarita CA 91355
    30 day value change: 17609
    rentzestimate (value): 5525
    
    
    row 464: 26122 Bella Santa Dr Santa Clarita CA 91355
    30 day value change: 10843
    rentzestimate (value): 2850
    
    
    row 465: 22362 Circle J Ranch Rd Santa Clarita CA 91350
    30 day value change: 12223
    rentzestimate (value): 3300
    
    
    row 466: 21717 Propello Dr Santa Clarita CA 91351
    30 day value change: 3886
    rentzestimate (value): 2200
    
    
    row 467: 21355 Placerita Canyon Rd Santa Clarita CA 91321
    30 day value change: 18786
    rentzestimate (value): 3700
    
    
    row 468: 25528 La Gosta Pl Santa Clarita CA 91355
    30 day value change: 7662
    rentzestimate (value): 2624
    
    
    row 469: 27067 Channel Ln Santa Clarita CA 91355
    30 day value change: 14681
    rentzestimate (value): 3200
    
    
    row 470: 24203 Wabuska St Santa Clarita CA 91321
    30 day value change: 5979
    rentzestimate (value): 2600
    
    
    row 471: 22223 Claibourne Ln Santa Clarita CA 91350
    30 day value change: 8651
    rentzestimate (value): 2850
    
    
    row 472: 24604 Sagecrest Cir Santa Clarita CA 91381
    30 day value change: -112
    rentzestimate (value): 3300
    
    
    row 473: 24506 Golden Oak Ln Santa Clarita CA 91321
    30 day value change: 2569
    rentzestimate (value): 6499
    
    
    row 474: 23876 Wildwood Canyon Rd Santa Clarita CA 91321
    30 day value change: 18685
    rentzestimate (value): 3300
    
    
    row 475: 21618 Oak Orchard Rd Santa Clarita CA 91321
    30 day value change: 2194
    rentzestimate (value): 3100
    
    
    row 476: 25625 Palma Alta Dr Santa Clarita CA 91355
    30 day value change: 5896
    rentzestimate (value): 2400
    
    
    row 477: 24234 Lema Dr Santa Clarita CA 91355
    30 day value change: 5924
    rentzestimate (value): 2500
    
    
    row 478: 22415 Cardiff Dr Santa Clarita CA 91350
    30 day value change: 5697
    rentzestimate (value): 3200
    
    
    row 479: 23944 Windward Ln Santa Clarita CA 91355
    30 day value change: 31951
    rentzestimate (value): 3800
    
    
    row 480: 22601 White Wing Way Santa Clarita CA 91350
    30 day value change: 963
    rentzestimate (value): 3200
    
    
    row 481: 25762 Alta Dr Santa Clarita CA 91355
    30 day value change: -4520
    rentzestimate (value): 3100
    
    
    row 482: 23153 1/2 8th St Santa Clarita CA 91321
    30 day value change: 26379
    rentzestimate (value): 3000
    
    
    row 483: 24166 Creekside Dr Santa Clarita CA 91321
    30 day value change: 11885
    rentzestimate (value): 3695
    
    
    row 484: 25301 Heather Vale St Santa Clarita CA 91350
    30 day value change: 6673
    rentzestimate (value): 3200
    
    
    row 485: 23926 Vía Hamaca Santa Clarita CA 91355
    30 day value change: 9023
    rentzestimate (value): 2900
    
    
    row 486: 25503 Langston St Santa Clarita CA 91355
    30 day value change: -3807
    rentzestimate (value): 2700
    
    
    row 487: 25538 Vía Pacifica Santa Clarita CA 91355
    30 day value change: -2336
    rentzestimate (value): 2800
    
    
    row 488: 21720 Placerita Canyon Rd Santa Clarita CA 91321
    30 day value change: -16074
    rentzestimate (value): 3195
    
    
    row 489: 27054 Clarence Ct Santa Clarita CA 91355
    30 day value change: 1971
    rentzestimate (value): 3200
    
    
    row 490: 24535 Farrow Dr Santa Clarita CA 91355
    30 day value change: 5921
    rentzestimate (value): 3295
    
    
    row 491: 24707 Napa Ct Santa Clarita CA 91355
    30 day value change: -25545
    rentzestimate (value): 9999
    
    
    row 492: 24243 Vista Hills Dr Santa Clarita CA 91355
    30 day value change: 6836
    rentzestimate (value): 5450
    
    
    row 493: 21157 Placeritos Blvd Santa Clarita CA 91321
    30 day value change: 162084
    rentzestimate (value): 3529
    
    
    row 494: 24912 Avenida Balita Santa Clarita CA 91355
    30 day value change: 7224
    rentzestimate (value): 2945
    
    
    row 495: 23598 Stillwater Pl Santa Clarita CA 91321
    30 day value change: 4192
    rentzestimate (value): 3100
    
    
    row 496: 1101-1105 Lilienthal Ln Redondo Beach CA 90278
    
    
    row 497: 1536 W 222nd St Torrance CA 90501
    30 day value change: 5477
    rentzestimate (value): 2800
    
    
    row 498: 3132 185th St Torrance CA 90504
    30 day value change: 12779
    rentzestimate (value): 2975
    
    
    row 499: 4109 Emerald St Torrance CA 90503
    30 day value change: -45562
    rentzestimate (value): 3000
    
    
    row 500: 2127 W 237th St Torrance CA 90501
    30 day value change: 9680
    rentzestimate (value): 3300
    
    
    row 501: 21734 Evalyn Ave Torrance CA 90503
    30 day value change: 3569
    rentzestimate (value): 3700
    
    
    row 502: 4202 Carmen St Torrance CA 90503
    30 day value change: 10838
    rentzestimate (value): 3400
    
    
    row 503: 18700 Crenshaw Blvd Torrance CA 90504
    30 day value change: 10436
    rentzestimate (value): 2800
    
    
    row 504: 22733 Anza Ave Torrance CA 90505
    30 day value change: 8079
    rentzestimate (value): 3395
    
    
    row 505: 2602 Cabrillo Ave Torrance CA 90501
    30 day value change: -5695
    30 day value change: -1068
    rentzestimate (value): 3200
    rentzestimate (value): 2900
    
    
    row 506: 1924 Middlebrook Rd Torrance CA 90501
    30 day value change: 10061
    rentzestimate (value): 3600
    
    
    row 507: 22741 Date Ave Torrance CA 90505
    30 day value change: 22512
    rentzestimate (value): 3000
    
    
    row 508: 19802 Tomlee Ave Torrance CA 90503
    30 day value change: 23089
    rentzestimate (value): 3400
    
    
    row 509: 2707 W 179th St Torrance CA 90504
    30 day value change: 14399
    rentzestimate (value): 2975
    
    
    row 510: 17119 Faysmith Ave Torrance CA 90504
    30 day value change: 5899
    rentzestimate (value): 3000
    
    
    row 511: 5405 Towers St Torrance CA 90503
    30 day value change: 17425
    rentzestimate (value): 3650
    
    
    row 512: 23003 Doris Way Torrance CA 90505
    30 day value change: 11080
    rentzestimate (value): 4500
    
    
    row 513: 1302 W 223rd St Torrance CA 90501
    30 day value change: -587
    rentzestimate (value): 3000
    
    
    row 514: 24245 Ward St Torrance CA 90505
    30 day value change: 9131
    rentzestimate (value): 2950
    
    
    row 515: 5321 Jacques St Torrance CA 90503
    30 day value change: 23080
    rentzestimate (value): 4000
    
    
    row 516: 1625 Maple Ave Torrance CA 90503
    30 day value change: 5392
    rentzestimate (value): 3200
    
    
    row 517: 2460 229th Pl Torrance CA 90505
    30 day value change: 27859
    rentzestimate (value): 3250
    
    
    row 518: 3462 W 170th St Torrance CA 90504
    30 day value change: 6243
    rentzestimate (value): 2900
    
    
    row 519: 4033 184th St Torrance CA 90504
    30 day value change: 18314
    rentzestimate (value): 2800
    
    
    row 520: 21122 Harvard Blvd Torrance CA 90501
    30 day value change: -2691
    rentzestimate (value): 2850
    
    
    row 521: 17801 Glenburn Ave Torrance CA 90504
    30 day value change: 9341
    rentzestimate (value): 2950
    
    
    row 522: 19417 Anza Ave Torrance CA 90503
    30 day value change: 11096
    rentzestimate (value): 3100
    
    
    row 523: 1551 W 206th St Torrance CA 90501
    30 day value change: 296
    rentzestimate (value): 2800
    
    
    row 524: 5028 Lee St Torrance CA 90503
    30 day value change: 16065
    rentzestimate (value): 3700
    
    
    row 525: 20357 Madison St Torrance CA 90503
    30 day value change: 7445
    rentzestimate (value): 3700
    
    
    row 526: 21146 Harvard Blvd Torrance CA 90501
    30 day value change: 106
    rentzestimate (value): 3000
    
    
    row 527: 1349 W 221st St Torrance CA 90501
    30 day value change: 6024
    rentzestimate (value): 2250
    
    
    row 528: 5013 Deelane St Torrance CA 90503
    30 day value change: 9080
    rentzestimate (value): 3600
    
    
    row 529: 3399 Candlewood Rd Torrance CA 90505
    30 day value change: 13722
    rentzestimate (value): 3601
    
    
    row 530: 18114 Manhattan Pl Torrance CA 90504
    30 day value change: 27286
    rentzestimate (value): 3000
    
    
    row 531: 17318 Casimir Ave Torrance CA 90504
    30 day value change: 12908
    rentzestimate (value): 2700
    
    
    row 532: 2365 Plaza del Amo Torrance CA 90501
    30 day value change: -3010
    rentzestimate (value): 2700
    
    
    row 533: 21730 Ladeene Ave Torrance CA 90503
    30 day value change: 7955
    rentzestimate (value): 3200
    
    
    row 534: 3853 W 231st Pl Torrance CA 90505
    30 day value change: 19853
    rentzestimate (value): 3700
    
    
    row 535: 3037 Lazy Meadow Dr Torrance CA 90505
    30 day value change: 10303
    rentzestimate (value): 3780
    
    
    row 536: 5457-5465 Sharynne Ln Torrance CA 90505
    30 day value change: 15639
    rentzestimate (value): 4812
    
    
    row 537: 18712 Felbar Ave Torrance CA 90504
    30 day value change: 10951
    rentzestimate (value): 2950
    
    
    row 538: 4298 Michelle Dr Torrance CA 90503
    30 day value change: -13945
    rentzestimate (value): 3900
    
    
    row 539: 21020 Ladeene Ave Torrance CA 90503
    30 day value change: 22238
    rentzestimate (value): 3000
    
    
    row 540: 3953 188th St Torrance CA 90504
    30 day value change: 39666
    rentzestimate (value): 3200
    
    
    row 541: 4299 W 190th St Torrance CA 90504
    30 day value change: 3759
    rentzestimate (value): 3500
    
    
    row 542: 4729 Deelane St Torrance CA 90503
    30 day value change: 7352
    rentzestimate (value): 3300
    
    
    row 543: 2130 Plaza del Amo Torrance CA 90501
    30 day value change: -4570
    30 day value change: -4256
    30 day value change: -2801
    30 day value change: -4570
    30 day value change: 1751
    30 day value change: 9382
    30 day value change: 1947
    30 day value change: -321
    30 day value change: -8651
    30 day value change: 548
    30 day value change: 1885
    30 day value change: -1255
    30 day value change: 2512
    30 day value change: -4466
    30 day value change: -3994
    30 day value change: -2049
    30 day value change: -5706
    30 day value change: 7667
    30 day value change: -82
    30 day value change: 350
    30 day value change: 214
    30 day value change: 2228
    30 day value change: 1053
    30 day value change: 10156
    30 day value change: -3287
    rentzestimate (value): 2600
    rentzestimate (value): 2800
    rentzestimate (value): 2850
    rentzestimate (value): 2600
    rentzestimate (value): 2900
    rentzestimate (value): 2800
    rentzestimate (value): 2900
    rentzestimate (value): 2800
    rentzestimate (value): 2995
    rentzestimate (value): 2895
    rentzestimate (value): 2900
    rentzestimate (value): 2750
    rentzestimate (value): 2950
    rentzestimate (value): 2795
    rentzestimate (value): 2675
    rentzestimate (value): 2850
    rentzestimate (value): 2600
    rentzestimate (value): 2700
    rentzestimate (value): 2700
    rentzestimate (value): 2700
    rentzestimate (value): 2850
    rentzestimate (value): 2900
    rentzestimate (value): 3000
    rentzestimate (value): 2850
    rentzestimate (value): 2850
    
    
    row 544: 2445 W 232nd St Torrance CA 90501
    30 day value change: 39252
    rentzestimate (value): 4071
    
    
    row 545: 3706 W 224th St Torrance CA 90505
    30 day value change: 5440
    rentzestimate (value): 3150
    
    
    row 546: 4730 Newton St Torrance CA 90505
    30 day value change: 21213
    rentzestimate (value): 3992
    
    
    row 547: 21832 Barbara St Torrance CA 90503
    30 day value change: 14631
    rentzestimate (value): 4200
    
    
    


```python
# check new dataframe
final_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
      <th>rentzestimate</th>
      <th>valuechange</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20825166</td>
      <td>1010 Omer Ln</td>
      <td>Burbank CA 91502</td>
      <td>34.167726</td>
      <td>-118.305972</td>
      <td>0</td>
      <td>862895.0</td>
      <td>906040.0</td>
      <td>819750.0</td>
      <td>704,400</td>
      <td>378788.0</td>
      <td>2017</td>
      <td>1944.0</td>
      <td>6592</td>
      <td>1612.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>2500</td>
      <td>23936</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20065948</td>
      <td>2601 W Oak St</td>
      <td>Burbank CA 91505</td>
      <td>34.161428</td>
      <td>-118.331196</td>
      <td>0</td>
      <td>1064774.0</td>
      <td>1118013.0</td>
      <td>1011535.0</td>
      <td>704,400</td>
      <td>560430.0</td>
      <td>2017</td>
      <td>1977.0</td>
      <td>6267</td>
      <td>2161.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>3900</td>
      <td>40688</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20054209</td>
      <td>907 E Orange Grove Ave</td>
      <td>Burbank CA 91501</td>
      <td>34.190172</td>
      <td>-118.301154</td>
      <td>0</td>
      <td>816428.0</td>
      <td>857249.0</td>
      <td>775607.0</td>
      <td>704,400</td>
      <td>137700.0</td>
      <td>2017</td>
      <td>1938.0</td>
      <td>7453</td>
      <td>1006.0</td>
      <td>3.0</td>
      <td>1.0</td>
      <td>2800</td>
      <td>18408</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20049263</td>
      <td>214 S Lincoln St</td>
      <td>Burbank CA 91506</td>
      <td>34.161947</td>
      <td>-118.327251</td>
      <td>0</td>
      <td>758370.0</td>
      <td>796288.0</td>
      <td>720452.0</td>
      <td>704,400</td>
      <td>685000.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>7048</td>
      <td>1156.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2950</td>
      <td>-2574</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20060944</td>
      <td>1600 Tulare Ave</td>
      <td>Burbank CA 91504</td>
      <td>34.202723</td>
      <td>-118.328088</td>
      <td>0</td>
      <td>820865.0</td>
      <td>861908.0</td>
      <td>779822.0</td>
      <td>704,400</td>
      <td>211628.0</td>
      <td>2017</td>
      <td>1949.0</td>
      <td>8578</td>
      <td>1431.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>3100</td>
      <td>-786</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Save file into Clean Data folder
final_df.to_csv(f'../Clean_Data/5-2.Combined_zillow_data.csv')
```
#### 6-1.General_Housing_Info_Plot



```python
# Dependencies
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import seaborn as sns, numpy as np
from itertools import cycle, islice
```


```python
# File to load
fdata="../Clean_Data/5-2.Combined_zillow_data.csv"

# Read the Data
f_data=pd.read_csv(fdata, encoding = "ISO-8859-1")
f_data = f_data[["zpid", "address","city_state_zip","latitude","longitude","message_code","zestimate",
                 "rentzestimate","valuation_high","valuation_low",'valuechange',"home value index","tax assessment",
                 "tax assess year","year built","lot size","finished sq ft","bedrooms","bathrooms"]]
f_data.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>rentzestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>valuechange</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20825166</td>
      <td>1010 Omer Ln</td>
      <td>Burbank CA 91502</td>
      <td>34.167726</td>
      <td>-118.305972</td>
      <td>0</td>
      <td>862895</td>
      <td>2500.0</td>
      <td>906040</td>
      <td>819750</td>
      <td>23936.0</td>
      <td>704,400</td>
      <td>378788</td>
      <td>2017</td>
      <td>1944</td>
      <td>6592</td>
      <td>1612</td>
      <td>4</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20065948</td>
      <td>2601 W Oak St</td>
      <td>Burbank CA 91505</td>
      <td>34.161428</td>
      <td>-118.331196</td>
      <td>0</td>
      <td>1064774</td>
      <td>3900.0</td>
      <td>1118013</td>
      <td>1011535</td>
      <td>40688.0</td>
      <td>704,400</td>
      <td>560430</td>
      <td>2017</td>
      <td>1977</td>
      <td>6267</td>
      <td>2161</td>
      <td>4</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20054209</td>
      <td>907 E Orange Grove Ave</td>
      <td>Burbank CA 91501</td>
      <td>34.190172</td>
      <td>-118.301154</td>
      <td>0</td>
      <td>816428</td>
      <td>2800.0</td>
      <td>857249</td>
      <td>775607</td>
      <td>18408.0</td>
      <td>704,400</td>
      <td>137700</td>
      <td>2017</td>
      <td>1938</td>
      <td>7453</td>
      <td>1006</td>
      <td>3</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20049263</td>
      <td>214 S Lincoln St</td>
      <td>Burbank CA 91506</td>
      <td>34.161947</td>
      <td>-118.327251</td>
      <td>0</td>
      <td>758370</td>
      <td>2950.0</td>
      <td>796288</td>
      <td>720452</td>
      <td>-2574.0</td>
      <td>704,400</td>
      <td>685000</td>
      <td>2017</td>
      <td>1949</td>
      <td>7048</td>
      <td>1156</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20060944</td>
      <td>1600 Tulare Ave</td>
      <td>Burbank CA 91504</td>
      <td>34.202723</td>
      <td>-118.328088</td>
      <td>0</td>
      <td>820865</td>
      <td>3100.0</td>
      <td>861908</td>
      <td>779822</td>
      <td>-786.0</td>
      <td>704,400</td>
      <td>211628</td>
      <td>2017</td>
      <td>1949</td>
      <td>8578</td>
      <td>1431</td>
      <td>2</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using 30day value change to estimate full year growth rate
f_data['Housing Growth'] = f_data['valuechange']*12 / f_data['zestimate']
f_data.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>zpid</th>
      <th>address</th>
      <th>city_state_zip</th>
      <th>latitude</th>
      <th>longitude</th>
      <th>message_code</th>
      <th>zestimate</th>
      <th>rentzestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>valuechange</th>
      <th>home value index</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
      <th>Housing Growth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20825166</td>
      <td>1010 Omer Ln</td>
      <td>Burbank CA 91502</td>
      <td>34.167726</td>
      <td>-118.305972</td>
      <td>0</td>
      <td>862895</td>
      <td>2500.0</td>
      <td>906040</td>
      <td>819750</td>
      <td>23936.0</td>
      <td>704,400</td>
      <td>378788</td>
      <td>2017</td>
      <td>1944</td>
      <td>6592</td>
      <td>1612</td>
      <td>4</td>
      <td>2.0</td>
      <td>0.332870</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20065948</td>
      <td>2601 W Oak St</td>
      <td>Burbank CA 91505</td>
      <td>34.161428</td>
      <td>-118.331196</td>
      <td>0</td>
      <td>1064774</td>
      <td>3900.0</td>
      <td>1118013</td>
      <td>1011535</td>
      <td>40688.0</td>
      <td>704,400</td>
      <td>560430</td>
      <td>2017</td>
      <td>1977</td>
      <td>6267</td>
      <td>2161</td>
      <td>4</td>
      <td>2.0</td>
      <td>0.458554</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20054209</td>
      <td>907 E Orange Grove Ave</td>
      <td>Burbank CA 91501</td>
      <td>34.190172</td>
      <td>-118.301154</td>
      <td>0</td>
      <td>816428</td>
      <td>2800.0</td>
      <td>857249</td>
      <td>775607</td>
      <td>18408.0</td>
      <td>704,400</td>
      <td>137700</td>
      <td>2017</td>
      <td>1938</td>
      <td>7453</td>
      <td>1006</td>
      <td>3</td>
      <td>1.0</td>
      <td>0.270564</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20049263</td>
      <td>214 S Lincoln St</td>
      <td>Burbank CA 91506</td>
      <td>34.161947</td>
      <td>-118.327251</td>
      <td>0</td>
      <td>758370</td>
      <td>2950.0</td>
      <td>796288</td>
      <td>720452</td>
      <td>-2574.0</td>
      <td>704,400</td>
      <td>685000</td>
      <td>2017</td>
      <td>1949</td>
      <td>7048</td>
      <td>1156</td>
      <td>2</td>
      <td>2.0</td>
      <td>-0.040729</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20060944</td>
      <td>1600 Tulare Ave</td>
      <td>Burbank CA 91504</td>
      <td>34.202723</td>
      <td>-118.328088</td>
      <td>0</td>
      <td>820865</td>
      <td>3100.0</td>
      <td>861908</td>
      <td>779822</td>
      <td>-786.0</td>
      <td>704,400</td>
      <td>211628</td>
      <td>2017</td>
      <td>1949</td>
      <td>8578</td>
      <td>1431</td>
      <td>2</td>
      <td>1.0</td>
      <td>-0.011490</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Get city data from city_state_zip
f_data['City'] = f_data.city_state_zip.str.split('\s+').str[1]
f_data = f_data.replace({"City": {'Los' : 'Los Angeles', 'Long' : 'Long Beach', 'Santa' : 'Santa Clarita', 'South':'Pasadena' }}) 
f_data['City'].value_counts()
```




    Glendale         65
    Los Angeles      59
    Palmdale         56
    Long Beach       55
    Santa Clarita    54
    Burbank          52
    Torrance         51
    Pasadena         51
    Alhambra         50
    Inglewood        50
    Name: City, dtype: int64




```python
# save file with estimate growth rate
f_data.to_csv(f'../Clean_Data/5-3.Combined_zillow_data_with_growthrate.csv')
```


```python
# group data by city and find the average housing growth for each cuty
housing_growth_df = f_data.groupby(["City"])['Housing Growth'].agg(['mean']).sort_index().reset_index()
housing_growth_df = housing_growth_df.rename(columns={"mean":"Housing_Growth_Avg"})

# set the plot x_axis, y_axis, title and label 
sns.set_style("whitegrid")
plt.figure(figsize=(10,6))
sns.barplot(x="City", y="Housing_Growth_Avg", data=housing_growth_df, palette=sns.color_palette("Set3", 19))
plt.xticks(rotation=45)
plt.xlabel("City")
plt.ylabel("Percent of 1 Year Housing Growth(%)")
plt.title("1-Year Average Housing Growth Rate by City")

# Save the figure
plt.savefig("../Clean_Data/6-1.Ave_Housing_Growth_by_City.png")
plt.show()
```


![png](Clean_Data/6-1.Ave_Housing_Growth_by_City.png)



```python
# group data by city and find the average housing growth for each cuty
rent_price_df = f_data.groupby(["City"])["rentzestimate"].agg(['mean']).sort_index().reset_index()
rent_price_df = rent_price_df.rename(columns={"mean":"Rent_Price_Avg"})

# set the plot x_axis, y_axis, title and label 
sns.set_style("whitegrid")
plt.figure(figsize=(10,6))
sns.barplot(x="City", y="Rent_Price_Avg", data=rent_price_df, palette=sns.color_palette("Set3", 19))
plt.xticks(rotation=45)
plt.xlabel("City")
plt.ylabel("Average Rent Price")
plt.title("Average Rent Price by City")

# Save the figure
plt.savefig("../Clean_Data/6-1.Ave_Rent_Price_by-City.png")
plt.show()
```


![png](Clean_Data/6-1.Ave_Rent_Price_by-City.png)



```python
# group data by city and find the average housing growth for each cuty
price_df = f_data.groupby(["City"])["zestimate"].agg(['mean']).sort_index().reset_index()
price_df = price_df.rename(columns={"mean":"House_Price_Avg"})

# set the plot x_axis, y_axis, title and label 
sns.set_style("whitegrid")
plt.figure(figsize=(10,6))
sns.barplot(x="City", y="House_Price_Avg", data=price_df, palette=sns.color_palette("Set3", 19))
plt.xticks(rotation=45)
plt.xlabel("City")
plt.ylabel("Average House Price")
plt.title("Average House Price by City")

# Save the figure
plt.savefig("../Clean_Data/6-1.Ave_House_Price_by_City.png")
plt.show()
```


![png](Clean_Data/6-1.Ave_House_Price_by_City.png)

#### 6-2.Addl_Analysis_with_Real_Data



```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import seaborn as sns, numpy as np
from itertools import cycle, islice
```


```python
##Loading Data in
import pandas as pd
zillow=pd.read_csv('../Clean_Data/5-3.Combined_zillow_data_with_growthrate.csv',sep=',', encoding='latin-1')
```


```python
##Getting City Averages for Columns
zillow_gb=zillow.groupby('City').mean()
```


```python
##Changing data types so they are more  readable 
zillow_gb.zestimate=zillow_gb.zestimate.astype('long')
zillow_gb.valuation_high=zillow_gb.valuation_high.astype('long')
zillow_gb.valuation_low=zillow_gb.valuation_low.astype('long')
zillow_gb['tax assessment']=zillow_gb['tax assessment'].astype('long')
zillow_gb['tax assess year']=zillow_gb['tax assess year'].astype('int')
zillow_gb['lot size']=zillow_gb['lot size'].astype('long')
zillow_gb['finished sq ft']=zillow_gb['finished sq ft'].astype('long')
zillow_gb['year built']=zillow_gb['year built'].astype('long')
zillow_gb.bedrooms=zillow_gb.bedrooms.astype('int')
zillow_gb.bathrooms=zillow_gb.bathrooms.astype('int')
```


```python
zillow_gb_lat_lng=[['latitude','longitude']]
```


```python
##Deleting unnecessary columns
del zillow_gb['zpid']
del zillow_gb['latitude']
del zillow_gb['longitude']
del zillow_gb['message_code']
```


```python
##Calculating some new measures
#Price per Lot Size
zillow_gb['PP_lot']=zillow_gb.zestimate/zillow_gb['lot size']
zillow_gb.PP_lot=zillow_gb.PP_lot.astype('int')
#Price per house size
zillow_gb['PP_sqft']=zillow_gb.zestimate/zillow_gb['finished sq ft']
zillow_gb.PP_sqft=zillow_gb.PP_sqft.astype('int')
zillow_gb
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>zestimate</th>
      <th>rentzestimate</th>
      <th>valuation_high</th>
      <th>valuation_low</th>
      <th>valuechange</th>
      <th>tax assessment</th>
      <th>tax assess year</th>
      <th>year built</th>
      <th>lot size</th>
      <th>finished sq ft</th>
      <th>bedrooms</th>
      <th>bathrooms</th>
      <th>Housing Growth</th>
      <th>PP_lot</th>
      <th>PP_sqft</th>
    </tr>
    <tr>
      <th>City</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alhambra</th>
      <td>192.500000</td>
      <td>786966</td>
      <td>2758.840000</td>
      <td>829426</td>
      <td>742117</td>
      <td>18075.940000</td>
      <td>385167</td>
      <td>2017</td>
      <td>1946</td>
      <td>19314</td>
      <td>1731</td>
      <td>2</td>
      <td>2</td>
      <td>0.265623</td>
      <td>40</td>
      <td>454</td>
    </tr>
    <tr>
      <th>Burbank</th>
      <td>25.500000</td>
      <td>1125583</td>
      <td>4187.500000</td>
      <td>1189356</td>
      <td>1060698</td>
      <td>11585.269231</td>
      <td>552952</td>
      <td>2017</td>
      <td>1957</td>
      <td>39165</td>
      <td>2134</td>
      <td>3</td>
      <td>2</td>
      <td>0.132308</td>
      <td>28</td>
      <td>527</td>
    </tr>
    <tr>
      <th>Glendale</th>
      <td>85.000000</td>
      <td>1137447</td>
      <td>3567.292308</td>
      <td>1211146</td>
      <td>1063506</td>
      <td>21903.676923</td>
      <td>566964</td>
      <td>2017</td>
      <td>1946</td>
      <td>12030</td>
      <td>2093</td>
      <td>3</td>
      <td>2</td>
      <td>0.222126</td>
      <td>94</td>
      <td>543</td>
    </tr>
    <tr>
      <th>Inglewood</th>
      <td>142.500000</td>
      <td>717422</td>
      <td>2734.500000</td>
      <td>798782</td>
      <td>667456</td>
      <td>5637.620000</td>
      <td>280203</td>
      <td>2017</td>
      <td>1949</td>
      <td>12584</td>
      <td>1964</td>
      <td>3</td>
      <td>2</td>
      <td>0.098407</td>
      <td>57</td>
      <td>365</td>
    </tr>
    <tr>
      <th>Long Beach</th>
      <td>245.000000</td>
      <td>643798</td>
      <td>2456.927273</td>
      <td>688384</td>
      <td>602054</td>
      <td>8054.672727</td>
      <td>360702</td>
      <td>2017</td>
      <td>1940</td>
      <td>7511</td>
      <td>1704</td>
      <td>3</td>
      <td>2</td>
      <td>0.164882</td>
      <td>85</td>
      <td>377</td>
    </tr>
    <tr>
      <th>Los Angeles</th>
      <td>297.271186</td>
      <td>770387</td>
      <td>2779.017241</td>
      <td>826419</td>
      <td>721323</td>
      <td>8573.293103</td>
      <td>264671</td>
      <td>2017</td>
      <td>1929</td>
      <td>14589</td>
      <td>1808</td>
      <td>3</td>
      <td>2</td>
      <td>0.160462</td>
      <td>52</td>
      <td>426</td>
    </tr>
    <tr>
      <th>Palmdale</th>
      <td>358.500000</td>
      <td>332900</td>
      <td>2145.796296</td>
      <td>351534</td>
      <td>314708</td>
      <td>2855.890909</td>
      <td>231949</td>
      <td>2017</td>
      <td>1983</td>
      <td>18357</td>
      <td>1940</td>
      <td>3</td>
      <td>2</td>
      <td>0.114943</td>
      <td>18</td>
      <td>171</td>
    </tr>
    <tr>
      <th>Pasadena</th>
      <td>412.000000</td>
      <td>1779256</td>
      <td>5561.901961</td>
      <td>1903052</td>
      <td>1652609</td>
      <td>4663.000000</td>
      <td>773550</td>
      <td>2017</td>
      <td>1944</td>
      <td>24416</td>
      <td>5378</td>
      <td>3</td>
      <td>3</td>
      <td>0.110612</td>
      <td>72</td>
      <td>330</td>
    </tr>
    <tr>
      <th>Santa Clarita</th>
      <td>464.500000</td>
      <td>759555</td>
      <td>3511.407407</td>
      <td>806203</td>
      <td>712300</td>
      <td>11370.055556</td>
      <td>548975</td>
      <td>2017</td>
      <td>1980</td>
      <td>35783</td>
      <td>2401</td>
      <td>3</td>
      <td>2</td>
      <td>0.163195</td>
      <td>21</td>
      <td>316</td>
    </tr>
    <tr>
      <th>Torrance</th>
      <td>517.000000</td>
      <td>897399</td>
      <td>3295.117647</td>
      <td>947420</td>
      <td>847064</td>
      <td>10133.588235</td>
      <td>437124</td>
      <td>2017</td>
      <td>1961</td>
      <td>18485</td>
      <td>1903</td>
      <td>3</td>
      <td>2</td>
      <td>0.138005</td>
      <td>48</td>
      <td>471</td>
    </tr>
  </tbody>
</table>
</div>




```python
##Getting city house prices for box and whisker plots 
zillow_box=zillow[['City','zestimate']]
```


```python
##Getting city house prices for box and whisker plots 
Glendale=zillow_box[zillow_box['City']=='Glendale']     
Burbank=zillow_box[zillow_box['City']=='Burbank'] 
Inglewood=zillow_box[zillow_box['City']=='Inglewood'] 
Alhambra=zillow_box[zillow_box['City']=='Alhambra'] 
Pasadena=zillow_box[zillow_box['City']=='Pasadena'] 
Long_Beach=zillow_box[zillow_box['City']=='Long Beach'] 
Los_Angeles=zillow_box[zillow_box['City']=='Los Angeles'] 
Palmdale=zillow_box[zillow_box['City']=='Palmdale'] 
Santa_Clarita=zillow_box[zillow_box['City']=='Santa Clarita'] 
Torrance=zillow_box[zillow_box['City']=='Torrance'] 
```


```python
##Getting city house prices for box and whisker plots 
##Getting only 50 per city the cities dont have matching records 
Glendale=Glendale.sample(n=50)
Burbank=Burbank.sample(n=50)
Inglewood=Inglewood.sample(n=50)
Alhambra=Alhambra.sample(n=50)
Pasadena=Pasadena.sample(n=50)
Long_Beach=Long_Beach.sample(n=50)
Los_Angeles=Los_Angeles.sample(n=50)
Palmdale=Palmdale.sample(n=50)
Santa_Clarita=Santa_Clarita.sample(n=50)
Torrance=Torrance.sample(n=50)
```


```python
##Getting city house prices for box and whisker plots 
Glendale.columns=['city','Glendal']
Burbank.columns=['city','Burbank']
Inglewood.columns=['city','Inglewood']
Alhambra.columns=['city','Alhambra']
Pasadena.columns=['city','Pasadena']
Long_Beach.columns=['city','Long_Beach']
Los_Angeles.columns=['city','Los_Angeles']
Palmdale.columns=['city','Palmdale']
Santa_Clarita.columns=['city','Santa_Clarita']
Torrance.columns=['city','Torrance']
```


```python
##Getting city house prices for box and whisker plots 
Glendale=Glendale.reset_index()
Burbank=Burbank.reset_index()
Inglewood=Inglewood.reset_index()
Alhambra=Alhambra.reset_index()
Pasadena=Pasadena.reset_index()
Long_Beach=Long_Beach.reset_index()
Los_Angeles=Los_Angeles.reset_index()
Palmdale=Palmdale.reset_index()
Santa_Clarita=Santa_Clarita.reset_index()
Torrance=Torrance.reset_index()
```


```python
##Getting city house prices for box and whisker plots 
df=pd.concat([Glendale.Glendal
           ,Burbank.Burbank
           ,Inglewood.Inglewood
           ,Alhambra.Alhambra
           ,Pasadena.Pasadena
           ,Long_Beach.Long_Beach
           ,Los_Angeles.Los_Angeles
           ,Palmdale.Palmdale
           ,Santa_Clarita.Santa_Clarita
           ,Torrance.Torrance],axis=1)
```


```python
##Drawing the box and whisker plots to see the variances in terms of prices 
import seaborn as sns
from matplotlib import pyplot as plt
plt.figure(figsize=(10,6))
sns.boxplot(data=df)
plt.ylim(0,5000000)
plt.ylabel("Price, USD")
plt.title('House Price Ranges per City')
plt.xticks(rotation=45)
plt.savefig("../Clean_Data/6-2.House_Price_Ranges_per_City.png")
plt.show()
```


![png](Clean_Data/6-2.House_Price_Ranges_per_City.png)



```python
# Drawing out Average Price Per sqft per City
# set the plot x_axis, y_axis, title and label 
sns.set_style("whitegrid")
plt.figure(figsize=(10,6))
sns.barplot(x=zillow_gb.index, y="PP_sqft", data=zillow_gb, palette=sns.color_palette("Set3", 19))
plt.xticks(rotation=45)
plt.ylabel("Price, USD")
plt.title("Average Price Per Squarefeet Per City")
plt.savefig("../Clean_Data/6-2.Average_Price_Per_Squarefeet_Per_City.png")
plt.show()
```


![png](Clean_Data/6-2.Average_Price_Per_Squarefeet_Per_City.png)



```python
# Drawing out Average Price Per lot per City
# set the plot x_axis, y_axis, title and label 
sns.set_style("whitegrid")
plt.figure(figsize=(10,6))
sns.barplot(x=zillow_gb.index, y="PP_lot", data=zillow_gb, palette=sns.color_palette("Set3", 19))
plt.xticks(rotation=45)
plt.ylabel("Price, USD")
plt.title("Average Price Per lot Per City")
plt.savefig("../Clean_Data/6-2.Average_Price_Per_lot_Per_City.png")
plt.show()
```


![png](Clean_Data/6-2.Average_Price_Per_lot_Per_City.png)



```python
# Drawing out Average year built per City
# set the plot x_axis, y_axis, title and label 
sns.set_style("whitegrid")
plt.figure(figsize=(10,6))
sns.barplot(x=zillow_gb.index, y="year built", data=zillow_gb, palette=sns.color_palette("Set3", 19))
plt.xticks(rotation=45)
plt.ylim(1920,1990)
plt.ylabel("Year")
plt.title("Average year built Per City")

plt.savefig("../Clean_Data/6-2.Average_year_built_Per_City.png")
plt.show()
```


![png](Clean_Data/6-2.Average_year_built_Per_City.png)


