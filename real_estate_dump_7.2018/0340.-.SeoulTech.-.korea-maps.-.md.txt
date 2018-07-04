Korea Maps
==========
South Korea regional boundary in simplified ESRI Shapefile, GeoJSON, and TopoJSON.


## Requirement
 - [GDAL](http://www.gdal.org)
 - [topojson](https://github.com/mbostock/topojson)

## Usage

### Generating Simplified ESRI Shapefile, GeoJSON, and TopoJSON
The make.sh shell script simplifies the original shape files and generates to the topojson files using topojson CLI. GeoJSON and ESRI Shapefile are generated from the topojson files.

 - ./shp : Original shape file
 - ./simplified_shp : Simplified shape file
 - ./topojson : TopoJson
 - ./geojson : GeoJson

 
```bash
$ ./make.sh
```

### Simplified Regional Boundary on Google Map.
Visit here(http://www.station3.co.kr/korea-maps).

Or run on the local machine(It requires Python).

```bash
$ ./run.sh
```

## Note

### Encoding conversion from the Shapefiles attributes(*.dbf)
The column names and attributes are written in Korean(euc-kr). But, it's difficult to use the non-english column names in Database or JavaScript code.
The shp/prepare_dbf.sh script convert the column names in English(utf-8) and
the attribute values in Korean(utf-8). The column names are as following.

 - state_code, state_name
 - city_code, city_name
 - dong_code, dong_name

### We Use It in Production
An awesome real estate service in South Korea, Dabang(http://www.dabangapp.com).

## Copyrights and License

### Author
Heehong Moon, Jeahyeok Song

### Data Source
한국 통계청(http://sgis.kostat.go.kr/statbd/statbd_03.vw)

### License
Copyright 2013 Station3, Inc under the Eclipse Public License.
