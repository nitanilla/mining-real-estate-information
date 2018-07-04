# jinfinigon
A java api for  the Infinigon's Social Analytical service
This api offers three iterable classes Timeline, Tweets, and Snaphots. 

## REQUIRED LIBRARIES

The only prequisit is that the API uses by default [json-simple-1.1.1.jar](https://github.com/fangyidong/json-simple) and [jinfinigon.jar](https://github.com/thanos/jinfinigon/raw/master/dist/jinfinigon_jar/jinfinigon.jar). Down load both jars and put it somewhere in your `CLASS_PATH`. 





## Connecting.
All the iterators take an optional Proxy object.


### Token 

For anonymous users the API is throttled. This allows you to either test against our system or create pages that are fairly static but calling these too frequently will get you an error such as: callback({"detail": "Request was throttled.Expected available in 85250 seconds."}); For any serious use you will need to use our simple token-based HTTP Authentication scheme. By default the API checks for an environment variable `INFINIGON_TOKEN`.  To use your own token strategy just override `getToken()` of `com.infinigongroup.api.InfinigonIterable`.






### Using a Proxy: 

```java
Proxy proxy = new Proxy(Proxy.Type.HTTP, new InetSocketAddress("10.38.89.25", 8080));
TimeSeries timeline = new Timeline("AAPL", Timeline.M, proxy);
for (Object timepoint : timeline) {
	System.out.println(timepoint);
}
		
```



## `com.infinigongroup.api.Timeline`

The iterable `Timeline` class yields timepoints of data for a given stream that enable you to build timeline charts for individual streams. 

### `Timeline` Data


```json
{	"date":"2015-08-19 00:45Z",
	"sentiment":0.0,
	"tweets":2
}
```

### `Timeline` Parameters

##### stream & resolution 
The constructor requires **stream** and **resolution** where:
* **stream** - is the **stream** id such as *AAPL* or *FDA*
* **resolution**  - Data is aggregated by minute, hour or day (for more see [Resolutions](http://realtime.infinigongroup.com/api/docs/#data_resolutions) ) so you can use:
 
 code | resolution
 --- | ---
 `TimeSeries.M` | for minutes
 `TimeSeries.H` | for hours
 `TimeSeries.d` | for days
 
##### start & stop 
Optionally you can give a date and time range by setting **start** and **stop**. **stop** parameter always defaults to now, while **start's** default value depends of the resolution on given.

 Format | Default Start Value |
 --- | --- 
 `TimeSeries.M` |	24 hours ago
 `TimeSeries.H` |	7 days ago
 `TimeSeries.d` |	30 days ago
    
    
You can specify the dates using [`java.utils.Date`](https://docs.oracle.com/javase/6/docs/api/java/util/Date.html) or you can also use a String in many formats (see [Date Formats] (http://realtime.infinigongroup.com/api/docs/#data_dates)). All times are by default **`UTC`** so you must be explicit and add the timezone. You can test your date and time values using: 

##### Time Delta

For the **start** parameter you can also give a *time delta*, specifying a period of time before the given (or default) **stop** date.

Period Code |	Period	| Example | Description 
--- | --- | --- | --- | ---
M |	minutes	| `"30M"` | starting thirty minutes ago
H |	hours	| `"8H"` | starting eight hours ago
d |	days	|`"5d"` | starting five days ago
w |	weeks	| `"2w"` | starting fortnight ago
m |	months	| `"3m"` | starting on the same date 3 months ago
y |	years	| `"1y"` | starting a year ago


### `Timeline` Examples

##### Reading minute timepoints for AAPL

```java
TimeSeries timeline = new Timeline("AAPL", TimeSeries.M, proxy);
int i =0;
for (Object timepoint : timeline) {
	System.out.print(i++ + ". ");
	System.out.println(timepoint);
}
```
```json
0. {"date":"2015-08-19 16:35Z","sentiment":0.67,"tweets":18}
1. {"date":"2015-08-19 16:36Z","sentiment":0.64,"tweets":39}
2. {"date":"2015-08-19 16:37Z","sentiment":0.67,"tweets":21}
3. {"date":"2015-08-19 16:38Z","sentiment":0.73,"tweets":37}
4. {"date":"2015-08-19 16:39Z","sentiment":0.63,"tweets":52}
5. {"date":"2015-08-19 16:40Z","sentiment":0.61,"tweets":28}
6. {"date":"2015-08-19 16:41Z","sentiment":0.66,"tweets":32}
7. {"date":"2015-08-19 16:42Z","sentiment":0.65,"tweets":37}
8. {"date":"2015-08-19 16:43Z","sentiment":0.63,"tweets":30}
9. {"date":"2015-08-19 16:44Z","sentiment":0.7,"tweets":44}
```

##### Reading hour of timepoints for AAPL

```java
TimeSeries timeline = new Timeline("AAPL", TimeSeries.H, proxy);
int i =0;
for (Object timepoint : timeline) {
	System.out.print(i++ + ". ");
	System.out.println(timepoint);
}
```
```json
0. {"date":"2015-08-10 17:00Z","sentiment":0.65,"tweets":2193}
1. {"date":"2015-08-10 18:00Z","sentiment":0.64,"tweets":2326}
2. {"date":"2015-08-10 19:00Z","sentiment":0.66,"tweets":2408}
3. {"date":"2015-08-10 20:00Z","sentiment":0.65,"tweets":2209}
4. {"date":"2015-08-10 21:00Z","sentiment":0.62,"tweets":1974}
5. {"date":"2015-08-10 22:00Z","sentiment":0.63,"tweets":1857}
6. {"date":"2015-08-10 23:00Z","sentiment":0.64,"tweets":1762}
7. {"date":"2015-08-11 00:00Z","sentiment":0.63,"tweets":1671}
8. {"date":"2015-08-11 01:00Z","sentiment":0.63,"tweets":1665}
9. {"date":"2015-08-11 02:00Z","sentiment":0.63,"tweets":1874}
```

##### Reading day of timepoints for AAPL

```java
TimeSeries timeline = new Timeline("AAPL", TimeSeries.d, proxy);
int i =0;
for (Object timepoint : timeline) {
	System.out.print(i++ + ". ");
	System.out.println(timepoint);
}
```
```json
0. {"date":"2015-07-22 00:00Z","sentiment":0.62,"tweets":26528}
1. {"date":"2015-07-23 00:00Z","sentiment":0.64,"tweets":22045}
2. {"date":"2015-07-24 00:00Z","sentiment":0.65,"tweets":24992}
3. {"date":"2015-07-25 00:00Z","sentiment":0.63,"tweets":29631}
4. {"date":"2015-07-26 00:00Z","sentiment":0.42,"tweets":1436}
5. {"date":"2015-07-27 00:00Z","sentiment":0.61,"tweets":11123}
6. {"date":"2015-07-28 00:00Z","sentiment":0.65,"tweets":26182}
7. {"date":"2015-07-29 00:00Z","sentiment":0.66,"tweets":24080}
8. {"date":"2015-07-30 00:00Z","sentiment":0.66,"tweets":42599}
9. {"date":"2015-07-31 00:00Z","sentiment":0.63,"tweets":52068
```


##### Reading last 4 days of day of timepoints for AAPL

```java
TimeSeries timeline = new Timeline("AAPL", TimeSeries.d, proxy).start("4d");
int i =0;
for (Object timepoint : timeline) {
	System.out.print(i++ + ". ");
	System.out.println(timepoint);
}
```
```json
0. {"date":"2015-08-17 00:00Z","sentiment":0.65,"tweets":41620}
1. {"date":"2015-08-18 00:00Z","sentiment":0.66,"tweets":41506}
2. {"date":"2015-08-19 00:00Z","sentiment":0.66,"tweets":42823}
3. {"date":"2015-08-20 00:00Z","sentiment":0.68,"tweets":28244}
```

##### Reading minute data from a given time of day for AAPL

```java
TimeSeries timeline = new Timeline("AAPL", TimeSeries.M).start("2015-08-19 12:34 EST").stop("2015-08-19 12:41 EST");
int i =0;
for (Object timepoint : timeline) {
	System.out.print(i++ + ". ");
	System.out.println(timepoint);
}
```
```json
0. {"date":"2015-08-19 17:34Z","sentiment":0.66,"tweets":32}
1. {"date":"2015-08-19 17:35Z","sentiment":0.61,"tweets":36}
2. {"date":"2015-08-19 17:36Z","sentiment":0.74,"tweets":31}
3. {"date":"2015-08-19 17:37Z","sentiment":0.68,"tweets":41}
4. {"date":"2015-08-19 17:38Z","sentiment":0.72,"tweets":36}
5. {"date":"2015-08-19 17:39Z","sentiment":0.53,"tweets":19}
6. {"date":"2015-08-19 17:40Z","sentiment":0.72,"tweets":32}
7. {"date":"2015-08-19 17:41Z","sentiment":0.6,"tweets":35}
```


## `com.infinigongroup.api.Tweets`

You can use the Tweets iterator  to request tweets from any stream for a given period in time.

### `Tweet` Data

```json
 { 	"postedTime":"2015-08-21T00:42:08.000Z",
 	"author":"DeltaBravo33",
 	"text":"Instagram : by airbus.driver - #Qantas #QantasAirways #melbourneairport #melbourne #boeing #boeing737 #b737 #737 #m\u2026 http:\/\/t.co\/7TgGML73aA",
 	"avatar":"https:\/\/pbs.twimg.com\/profile_images\/589500634149343232\/wcMsP73m_normal.jpg"
 }
```

### `Tweet` Parameters

##### stream 
The constructor requires **stream** and **resolution** where:
* **stream** - is the **stream** id such as *AAPL* or *FDA*



 
##### start & stop 
As with Timeline you can give a date and time range by setting **start** and **stop**. **stop** parameter always defaults to now, while **start's** default value is the start of the current minute.


    
    
You can specify the dates using [`java.utils.Date`](https://docs.oracle.com/javase/6/docs/api/java/util/Date.html) or you can also use a String in many formats (see [Date Formats] (http://realtime.infinigongroup.com/api/docs/#data_dates)). All times are by default **`UTC`** so you must be explicit and add the timezone. You can test your date and time values using: 

##### Time Delta

For the **start** parameter you can also give a *time delta*, specifying a period of time before the given (or default) **stop** date.

Period Code |	Period	| Example | Description 
--- | --- | --- | --- | ---
M |	minutes	| `"30M"` | starting thirty minutes ago
H |	hours	| `"8H"` | starting eight hours ago
d |	days	|`"5d"` | starting five days ago
w |	weeks	| `"2w"` | starting fortnight ago
m |	months	| `"3m"` | starting on the same date 3 months ago
y |	years	| `"1y"` | starting a year ago

 


### `Tweet` Examples

##### Reading minute tweets for BA

```java
TimeSeries tweets = new Tweets("FB", TimeSeries.M, proxy);
int i =0;
for (Object tweet : tweets) {
	System.out.print(i++ + ". ");
	System.out.println(tweet);
}
```
```json
0. {"postedTime":"2015-08-21T00:42:00.000Z","author":"DeltaBravo33","text":"Instagram : by world_aviation99 - Good night!! Lufthansa Cargo Boeing 777F landing at Frankfurt intl. #Boeing #avpo\u2026 http:\/\/t.co\/iZWmjWSuUz","avatar":"https:\/\/pbs.twimg.com\/profile_images\/589500634149343232\/wcMsP73m_normal.jpg"}
1. {"postedTime":"2015-08-21T00:42:05.000Z","author":"kevinagipavuc","text":"RT @josephuhanokov: ? ??????? ?????? ??????????? ?? ?????????? Boeing ??? ????????? ???????? ?? ???????","avatar":"https:\/\/pbs.twimg.com\/profile_images\/523784246427537408\/OqWKikgU_normal.png"}
2. {"postedTime":"2015-08-21T00:42:08.000Z","author":"DeltaBravo33","text":"Instagram : by world_aviation99 - Good night!! Lufthansa Cargo Boeing 777F landing at Frankfurt intl. #Boeing #avpo\u2026 http:\/\/t.co\/0FZsSYizdK","avatar":"https:\/\/pbs.twimg.com\/profile_images\/589500634149343232\/wcMsP73m_normal.jpg"}
3. {"postedTime":"2015-08-21T00:42:08.000Z","author":"DeltaBravo33","text":"Instagram : by airbus.driver - #Qantas #QantasAirways #melbourneairport #melbourne #boeing #boeing737 #b737 #737 #m\u2026 http:\/\/t.co\/7TgGML73aA","avatar":"https:\/\/pbs.twimg.com\/profile_images\/589500634149343232\/wcMsP73m_normal.jpg"}


```

## `com.infinigongroup.api.Snapshot`


`Snapshot` - Returns aggregation data for a selection of streams. Use this API to generate grids, maps, heat trees and clouds for groups of streams. 


### `Snapshot` Data


```json
{
			"description": "Chevron Corporation",
			"sentiment": 0.558823529411764,
			"tags": [
				"Equities",
				"Energy",
				"SP500",
				"Oil & Gas",
				"DJ30"
			],
			"timestamp": {
				"$date": 1440164723564
			},
			"symbol": "CVX",
			"clout": 1292,
			"words": [
				[
					"chevron",
					18
				],
				[
					"oil",
					3
				],
				[
					"morningword",
					3
				],
				[
					"slick",
					3
				],
				[
					"xom",
					3
				],
				[
					"cvx",
					3
				],
				[
					"negra",
					2
				],
				[
					"loma",
					2
				],
				[
					"superpozo",
					2
				],
				[
					"negro",
					2
				]
			],
			"activity": 34,
			"change_5": 14,  
			"variance": -67,
			"change_3": 69,
			"change_10": 8
		}
```

### `Snapshot` Fields

##### `last_request`
    Gives you the timestamp in java.util.Date  of the last update. 
    
    
### `Snapshot` Parameters


##### `since`
    Use this parameter to retrieve streams that have had activity since some given date. See the documentation on start. See above documentation on `start`.
    


    
##### `streams` 

    You can specify one or more streams, comma delimited, the default is all streams with available data. 
```java   
for (Object snapshot : new Snapshots().streams("AAPL", "GOOG")) {
    System.out.print(i++ + ". ");
    System.out.println(snapshot);
    if (i == 20) break;
}
```

```json
0. {"clout":9278,"sentiment":0.6392857143,"symbol":"AAPL","change_10":7,"activity":6537,"change_3":18,"variance":-94,"change_5":18,"words":[["iphone",118.0],["ipad",86.0],["apple",68.0],["gameinsight",36.0],["full",29.0],["steve",27.0],["jobs",27.0],["ipadgames",27.0],["read",19.0],["16gb",17.0]],"description":"Apple Inc","tags":["Personal Computers","Equities","SP500","Technology","PWTRADEWATCHLIST"],"timestamp":{"$date":1440282041210}}
1. {"clout":5976,"sentiment":0.7231638418,"symbol":"GOOG","change_10":13,"activity":3351,"change_3":34,"variance":-92,"change_5":20,"words":[["google",105.0],["play",22.0],["servers",19.0],["allaboutgoogle",19.0],["datacenter",19.0],["loses",18.0],["disponible",18.0],["data",18.0],["app",15.0],["consecutive",15.0]],"description":"Google Inc.","tags":["Equities","SP500","Technology","Internet Information Providers","PWTRADEWATCHLIST"],"timestamp":{"$date":1440282020217}}
```

    
##### `tags`
    Instead of specifying streams you can specify category or groups of streams that we call tags. The notation is a little more developed that just a comma delimited list, so I'm going to show you some examples:

* `{DJ30}{Energy}*`  Streams that are in the energy sector and belong to the DJ30. 
* `<DJ30>` Streams that are NOT in the DJ30.
* `{Energy}<DJ30>*` Streams that are in the energy sector and DO NOT belong to the DJ30.
* `{Energy}<DJ30>*{SP500}|` (Streams that are in energy sector but do not belong to the DJ30) OR ( those that belong to the SP500).


###### Snapshots of streams that are in the energy sector and belong to the DJ30. 

```java    
for (Object snapshot : new Snapshots().tags("{DJ30}{Energy}*")) {
    System.out.print(i++ + ". ");
    System.out.println(snapshot);
    if (i == 20) break;
}
```

```json
0. {"clout":1557,"sentiment":0.575,"symbol":"XOM","change_10":-42,"activity":155,"change_3":-47,"variance":-72,"change_5":-39,"words":[["mobil",30.0],["baru",6.0],["ini",6.0],["drive",6.0],["coba",6.0],["mau",6.0],["test",6.0],["iims",6.0],["pameran",6.0],["bisa",6.0]],"description":"Exxon Mobil Corporation","tags":["Equities","Energy","SP500","Oil & Gas","DJ30"],"timestamp":{"$date":1440282187760}}
1. {"clout":1356,"sentiment":0.5666666667,"symbol":"CVX","change_10":15,"activity":30,"change_3":-23,"variance":25,"change_5":15,"words":[["chevron",26.0],["etsy",7.0],["blue",4.0],["via",2.0],["pnnfi0xrsb",2.0],["yellow",2.0],["female",2.0],["help",2.0],["transfer",2.0],["white",2.0]],"description":"Chevron Corporation","tags":["Equities","Energy","SP500","Oil & Gas","DJ30"],"timestamp":{"$date":1440282211473}}

```


###### Snapshots of streams that are in the energy sector and DO NOT belong to the DJ30.

```java    
for (Object snapshot : new Snapshots().tags("{Energy}<DJ30>*")) {
    System.out.print(i++ + ". ");
    System.out.println(snapshot);
    if (i == 20) break;
}
```

```json

0. {"clout":98,"sentiment":0.0,"symbol":"SGY","change_10":3500,"activity":2,"change_3":-100,"variance":0,"change_5":-100,"words":[],"description":"Stone Energy Corp.","tags":["Equities","Energy","Independent Oil & Gas","AUTOGEN","NYSE"],"timestamp":{"$date":1440282083093}}
1. {"clout":93,"sentiment":0.25,"symbol":"E","change_10":-26,"activity":4,"change_3":-100,"variance":-13,"change_5":-100,"words":[],"description":"Eni S.P.A.","tags":["Major Integrated Oil & Gas","AUTOGEN","Equities","Energy","PWTRADEWATCHLIST","NYSE"],"timestamp":{"$date":1440282247729}}

```




As you can see we are using Reverse Polish Notation.

    Sets of tags you want are defined using comma delimited tags in braces {}
    Sets of tags you don't want are defined using comma delimited tags in braces angle brackets <>
    You can union (or OR) your sets using the | pipe symbol.
    You can intersect (or AND) your sets using the * star symbol.

Just remember in Reverse Polish Notation

    operandA operandB operator = operandA operator operandB
    operandA operandB operator1 operandC operator2 = (operandA operator1 operandB) operator2 operandC
    operandA operandB operator1 operandC operandD operator2 operator3 = (operandA operator1 operandB) operator3 (operandC operator2 operandD)

For more on RPN see http://en.wikipedia.org/wiki/Reverse_Polish_notation.

##### `words`
    Just as with `tags` you can filter by words in the word cloud using our RPN. The setting is character case insensitive. For instance 
    '{buy}<best buy>*{fda}{approval}*|`
Returns the data for streams whose word cloud **contains**  `buy` but **not** `best buy`, **or**  any streams  whose word cloud **contains** `fda` **and** `approval`. 
    
```java    
for (Object snapshot : new Snapshots().words("{buy}<best buy>*{fda}{approval}*|")) {
    System.out.print(i++ + ". ");
    System.out.println(snapshot);
    if (i == 20) break;
}
```

```json
0. {"clout":2972,"sentiment":0.6,"symbol":"NDAQ","change_10":104,"activity":65,"change_3":119,"variance":18,"change_5":138,"words":[["nasdaq",65.0],["inc",35.0],["corp",6.0],["rating",4.0],["zacks",4.0],["buy",4.0],["stock",4.0],["upgraded",3.0],["sells",3.0],["lifted",2.0]],"description":"Nasdaq OMX Group Inc","tags":["Diversified Investments","SP500","Financial","Equities"],"timestamp":{"$date":1440282934625}}
1. {"clout":936,"sentiment":0.3,"symbol":"NOK","change_10":-3,"activity":96,"change_3":8,"variance":-72,"change_5":-3,"words":[["nokia",28.0],["business",9.0],["german",9.0],["car",9.0],["sale",9.0],["consortium",9.0],["maps",9.0],["confirms",9.0],["buy",4.0],["smoothblink2konga",4.0]],"description":"Nokia Corporation","tags":["Equities","Communication Equipment","Technology"],"timestamp":{"$date":1440282989083}}
2. {"clout":1412,"sentiment":0.3684210526,"symbol":"BBY","change_10":10,"activity":38,"change_3":44,"variance":0,"change_5":21,"words":[["buy",32.0],["best",32.0],["time",2.0]],"description":"Best Buy Co. Inc.","tags":["Services","Equities","SP500","PWTRADEWATCHLIST","Electronics Stores"],"timestamp":{"$date":1440283001402}}
3. {"clout":1246,"sentiment":0.4545454545,"symbol":"URBN","change_10":73,"activity":33,"change_3":74,"variance":31,"change_5":26,"words":[["outfitters",20.0],["urban",20.0],["swags",5.0],["fleeks",5.0],["sensible",5.0],["dad",5.0],["buy",5.0],["sir",5.0],["amp",5.0],["dankcharnley",5.0]],"description":"Urban Outfitters Inc","tags":["Services","Equities","SP500","PWTRADEWATCHLIST","Apparel Stores"],"timestamp":{"$date":1440283019757}}
4. {"clout":4853,"sentiment":0.5784313725,"symbol":"TGT","change_10":138,"activity":102,"change_3":427,"variance":164,"change_5":356,"words":[["target",99.0],["best",57.0],["price",55.0],["offer",12.0],["freeshipping",10.0],["get",9.0],["clothing",9.0],["amp",7.0],["mossimo",7.0],["buy",7.0]],"description":"Target Corp.","tags":["PWTRADEW","Equities","Morgan Stanley Watchlist","Variety Stores","Discount","Services","SP500"],"timestamp":{"$date":1440283019889}}
5. {"clout":35092,"sentiment":0.6952054795,"symbol":"SFS","change_10":9,"activity":878,"change_3":35,"variance":-15,"change_5":23,"words":[["smart",819.0],["full",126.0],["android",115.0],["phone",114.0],["core",93.0],["unlocked",86.0],["dual",73.0],["read",67.0],["apple",64.0],["mobile",58.0]],"description":"Smart","tags":["NYSE","Equities"],"timestamp":{"$date":1440283021015}}
6. {"clout":4033,"sentiment":0.48,"symbol":"KRFT","change_10":-16,"activity":199,"change_3":7,"variance":-50,"change_5":-1,"words":[["oreo",70.0],["nabisco",7.0],["food_you_love",4.0],["cookies",3.0],["vie",3.0],["xkingpunk",3.0],["nini_oreo",2.0],["itsfoodporn",2.0],["cheesecake",2.0],["vsak3jq71a",2.0]],"description":"Kraft Foods Group Inc","tags":["Equities","Food - Major Diversified","SP500","Consumer Goods","Morgan Stanley Watc"],"timestamp":{"$date":1440283021271}}
7. {"clout":8726,"sentiment":0.6940298507,"symbol":"AAPL","change_10":2,"activity":6438,"change_3":-1,"variance":-94,"change_5":0,"words":[["iphone",114.0],["ipad",102.0],["apple",56.0],["full",38.0],["gameinsight",32.0],["ipadgames",31.0],["read",23.0],["16gb",18.0],["ebay",17.0],["case",15.0]],"description":"Apple Inc","tags":["Personal Computers","Equities","SP500","Technology","PWTRADEWATCHLIST"],"timestamp":{"$date":1440283021303}}
8. {"clout":9035,"sentiment":0.7012448133,"symbol":"BITCOIN","change_10":-33,"activity":242,"change_3":-37,"variance":-13,"change_5":-33,"words":[["bitcoin",235.0],["free",52.0],["freebitcoin",44.0],["satoshis",41.0],["earned",31.0],["robotcoingame",31.0],["total",31.0],["robot",31.0],["left",30.0],["btc",22.0]],"description":"Bitcoin","tags":["Bitcoin Information"],"timestamp":{"$date":1440283021514}}
9. {"clout":4475,"sentiment":0.3583333333,"symbol":"NFLX","change_10":20,"activity":1164,"change_3":73,"variance":-86,"change_5":42,"words":[["netflix",116.0],["chill",31.0],["watch",17.0],["amp",11.0],["bensetters",6.0],["multiple",6.0],["let",6.0],["times",6.0],["netfixandchill",5.0],["like",4.0]],"description":"NetFlix Inc.","tags":["Equities","Music & Video Stores","Level2","PWTRADEWATCHLIST","Services","SP500"],"timestamp":{"$date":1440283021636}}
``` 
    
 
    
##### `change_3`
    Use this parameter to filter by **percent change** in the last **3 minutes**. 
```java   
 for (Object snapshot : new Snapshots().change_3(180)) {
    System.out.print(i++ + ". ");
    System.out.println(snapshot);
    if (i == 20) break;
}
```       
        
```json        
0. {"clout":228,"sentiment":0.25,"symbol":"TSX:WJA","change_10":115,"activity":4,"change_3":614,"variance":1,"change_5":329,"words":[["kfll",2.0],["boeing",2.0],["aviationlovers",2.0],["avgeek",2.0],["livery",2.0],["tail",2.0],["plaid",2.0],["avporn",2.0],["westjet",2.0],["aviation",2.0]],"description":null,"tags":[],"timestamp":{"$date":1440282543164}}
1. {"clout":47,"sentiment":0.0,"symbol":"BGS","change_10":35,"activity":1,"change_3":349,"variance":167,"change_5":170,"words":[],"description":"B&G Foods Inc.","tags":["Equities","Consumer Goods","Processed & Packaged Goods"],"timestamp":{"$date":1440282543998}}
2. {"clout":47,"sentiment":0.0,"symbol":"PGR","change_10":260,"activity":1,"change_3":1100,"variance":10,"change_5":620,"words":[],"description":"Progressive Corp.","tags":["Property & Casualty Insurance","SP500","Financial","Equities"],"timestamp":{"$date":1440282604505}}
3. {"clout":91,"sentiment":0.0,"symbol":"SKYNEWS","change_10":300,"activity":1,"change_3":1234,"variance":482,"change_5":700,"words":[],"description":"Sky News","tags":["Publication"],"timestamp":{"$date":1440282615756}}
4. {"clout":44,"sentiment":0.0,"symbol":"KMB","change_10":30,"activity":1,"change_3":333,"variance":-55,"change_5":160,"words":[],"description":"Kimberly-Clark Corporation","tags":["Equities","SP500","Consumer Goods","Personal Products"],"timestamp":{"$date":1440282643536}}
5. {"clout":17,"sentiment":0.0,"symbol":"PNR","change_10":19,"activity":1,"change_3":294,"variance":238,"change_5":137,"words":[],"description":"Pentair Ltd.","tags":["Diversified Machinery","SP500","Equities","Industrial Goods"],"timestamp":{"$date":1440282729034}}
6. {"clout":46,"sentiment":0.0,"symbol":"FERGUSONTRACKER","change_10":129,"activity":20,"change_3":662,"variance":-93,"change_5":358,"words":[],"description":"Ferguson Situation","tags":["News"],"timestamp":{"$date":1440282745912}}
```

##### `change_5`
    Use this parameter to filter by **percent change** in the last **5 minutes**. 
```java   
 for (Object snapshot : new Snapshots().change_5(180)) {
    System.out.print(i++ + ". ");
    System.out.println(snapshot);
    if (i == 20) break;
}
```       
        
```json        
0. {"clout":55,"sentiment":0.0,"symbol":"UFC:WANDERLEISILVA","change_10":275,"activity":2,"change_3":-100,"variance":46,"change_5":275,"words":[],"description":null,"tags":[],"timestamp":{"$date":1440282676824}}
1. {"clout":46,"sentiment":0.0,"symbol":"FERGUSONTRACKER","change_10":129,"activity":20,"change_3":662,"variance":-93,"change_5":358,"words":[],"description":"Ferguson Situation","tags":["News"],"timestamp":{"$date":1440282745912}}
2. {"clout":27,"sentiment":0.0,"symbol":"TSX:BMO","change_10":312,"activity":1,"change_3":-100,"variance":302,"change_5":723,"words":[],"description":null,"tags":[],"timestamp":{"$date":1440282746616}}
3. {"clout":58,"sentiment":0.0,"symbol":"GT","change_10":66,"activity":1,"change_3":-100,"variance":-70,"change_5":232,"words":[],"description":"Goodyear Tire & Rubber Co","tags":["Equities","Rubber & Plastics","SP500","Consumer Goods"],"timestamp":{"$date":1440282766247}}
4. {"clout":55,"sentiment":0.0,"symbol":"TG","change_10":66,"activity":1,"change_3":452,"variance":200,"change_5":232,"words":[],"description":"Tredegar Corp.","tags":["Equities","Rubber & Plastics","Basic Materials","AUTOGEN","NYSE"],"timestamp":{"$date":1440282793676}}
5. {"clout":125,"sentiment":0.0,"symbol":"TSX:TRI","change_10":152,"activity":3,"change_3":459,"variance":201,"change_5":235,"words":[],"description":null,"tags":[],"timestamp":{"$date":1440282837295}}
6. {"clout":43,"sentiment":0.0,"symbol":"TSX:GMM.U","change_10":162,"activity":1,"change_3":773,"variance":-17,"change_5":424,"words":[],"description":null,"tags":[],"timestamp":{"$date":1440282857421}}
7. {"clout":124,"sentiment":0.0,"symbol":"DDS","change_10":224,"activity":4,"change_3":170,"variance":79,"change_5":386,"words":[["people",2.0],["dillard",2.0],["mall",2.0],["lot",2.0],["department",2.0],["rocking",2.0],["blast",2.0],["saw",2.0],["store",2.0],["cool",2.0]],"description":"Dillard's Inc","tags":["Equities","NYSE","Services","Department Stores"],"timestamp":{"$date":1440282859798}}
8. {"clout":78,"sentiment":0.0,"symbol":"FXI","change_10":295,"activity":2,"change_3":558,"variance":-64,"change_5":690,"words":[],"description":"FTSE China 25 Index Fund Ishares","tags":["Amex","Equities"],"timestamp":{"$date":1440282882266}}

``` 
##### `change_10`
    Use this parameter to filter by **percent change** in the last **10 minutes**. 

```java   
     for (Object snapshot : new Snapshots().change_3(300).change_5(180).change_10(300)) {
            System.out.print(i++ + ". ");
            System.out.println(snapshot);
            if (i == 20) break;
        }
```       
        
```json        
0. {"clout":55,"sentiment":0.0,"symbol":"CFN","change_10":586,"activity":1,"change_3":2186,"variance":101,"change_5":1272,"words":[],"description":"CareFusion Corporation","tags":["SAC List","Health Care","Medical\/Dental Instruments","Equities"],"timestamp":{"$date":1440282914323}}
1. {"clout":51,"sentiment":0.0,"symbol":"CCE","change_10":555,"activity":1,"change_3":2082,"variance":50,"change_5":1210,"words":[],"description":"Coca-Cola Enterprises","tags":["Beverages Non-Alcoholic","SP500","Consumer Goods","Equities"],"timestamp":{"$date":1440283054172}}
2. {"clout":83,"sentiment":0.0,"symbol":"MTB","change_10":300,"activity":2,"change_3":567,"variance":-97,"change_5":300,"words":[],"description":"M&T Bank Corporation","tags":["Equities","SP500","Financial","Regional - Northeast Banks"],"timestamp":{"$date":1440283056919}}
3. {"clout":48,"sentiment":0.0,"symbol":"TSX:TOG","change_10":2780,"activity":1,"change_3":9501,"variance":0,"change_5":5660,"words":[],"description":null,"tags":[],"timestamp":{"$date":1440283057520}}
4. {"clout":48,"sentiment":0.0,"symbol":"TSX:TMC","change_10":2780,"activity":1,"change_3":9501,"variance":0,"change_5":5660,"words":[],"description":null,"tags":[],"timestamp":{"$date":1440283057680}}
5. {"clout":98,"sentiment":0.0,"symbol":"TPVG","change_10":4700,"activity":2,"change_3":15900,"variance":0,"change_5":9501,"words":[],"description":"Triplepoint Venture Growth Bdc","tags":["NYSE","Equities"],"timestamp":{"$date":1440283057704}}
6. {"clout":48,"sentiment":0.0,"symbol":"TSX:SGY","change_10":1958,"activity":1,"change_3":6758,"variance":0,"change_5":4015,"words":[],"description":null,"tags":[],"timestamp":{"$date":1440283062709}}
7. {"clout":1639,"sentiment":0.6666666667,"symbol":"ZAGG","change_10":516,"activity":36,"change_3":414,"variance":1279,"change_5":550,"words":[["zagg",35.0],["ipad",33.0],["mini",33.0],["full",33.0],["apple",33.0],["gray",33.0],["retina",33.0],["space",33.0],["2nd",33.0],["book",33.0]],"description":"Zagg Inc.","tags":["Equities","NASDAQ","Specialty Retail","AUTOGEN","Consumer Non-Durables"],"timestamp":{"$date":1440283074787}}
8. {"clout":148,"sentiment":0.3333333333,"symbol":"WHLR","change_10":5301,"activity":3,"change_3":17900,"variance":0,"change_5":10700,"words":[["real",2.0],["estate",2.0],["wheeler",2.0],["whlr",2.0],["trust",2.0],["investment",2.0]],"description":"Wheeler Real Estate Investment","tags":["Equities","NASDAQ","REIT - Diversified","AUTOGEN","Real Estate"],"timestamp":{"$date":1440283099475}}
9. {"clout":148,"sentiment":0.3333333333,"symbol":"WHLRP","change_10":5301,"activity":3,"change_3":17900,"variance":0,"change_5":10700,"words":[["real",2.0],["estate",2.0],["wheeler",2.0],["whlr",2.0],["trust",2.0],["investment",2.0]],"description":"Wheeler Real Estate Investment","tags":["Nasdaq","Equities"],"timestamp":{"$date":1440283099601}}


``` 


##### `variance`
    Use this parameter to filter by **variance** for the hour. So if you used a value of 30 the Snapshot iterator would return data for streams that have 30% or more tweets than the average for that stream for the given hour for that day. This is useful for consumer companies such as Mac Donald's that typically have a higher rate at lunch times and in the evenings.
 
 

```java   

for (Object snapshot : new Snapshots().variance(3000)) {
    System.out.print(i++ + ". ");
    System.out.println(snapshot);
    if (i == 20) break;
}

```       
        
```json        
0. {"clout":729,"sentiment":0.125,"symbol":"URE","change_10":1687,"activity":16,"change_3":2133,"variance":9500,"change_5":2803,"words":[["ure",14.0],["someone",14.0],["like",14.0],["asks",14.0],["urpri",14.0],["birthday",14.0],["coliegestudent",14.0]],"description":"Ultra Real Estate Proshares","tags":["Amex","Equities"],"timestamp":{"$date":1440283328335}}
1. {"clout":8419,"sentiment":0.6889952153,"symbol":"BEAM","change_10":1537,"activity":209,"change_3":1519,"variance":22744,"change_5":1357,"words":[["vodka",208.0],["effen",208.0],["cent",201.0],["french",200.0],["trash",199.0],["montana",199.0],["throws",109.0],["iamakademiks",88.0],["throwing",82.0],["responds",82.0]],"description":"Beam Inc.","tags":["Equities","Beverages - Wineries & Distillers","SP500","Consumer Goods"],"timestamp":{"$date":1440283429252}}
2. {"clout":754,"sentiment":0.3529411765,"symbol":"WEATHER-SOYBEANS","change_10":281,"activity":17,"change_3":199,"variance":4917,"change_5":169,"words":[["tornado",12.0],["raiders",5.0],["minnesota",4.0],["watch",4.0],["vikings",3.0],["pregame",3.0],["field",3.0],["due",3.0],["lightning",3.0],["warning",3.0]],"description":"Soybeans US Crop","tags":["Commodities"],"timestamp":{"$date":1440283437478}}
3. {"clout":754,"sentiment":0.3529411765,"symbol":"WEATHER-CORN","change_10":284,"activity":17,"change_3":201,"variance":3257,"change_5":171,"words":[["tornado",12.0],["raiders",5.0],["minnesota",4.0],["watch",4.0],["vikings",3.0],["pregame",3.0],["field",3.0],["due",3.0],["lightning",3.0],["warning",3.0]],"description":"Corn","tags":["Commodities"],"timestamp":{"$date":1440283437576}}

``` 

    
##### `fields`
    You can specify which fields you want to retrieve using a comma delimited list. By default you get them all. The available fields are:

* activity
* change_3
* change_5
* change_10
* description
* sentiment
* variance
* words
* tags


```java   
for (Object snapshot : new Snapshots().variance(3000).fields("variance", "sentiment")) {
    System.out.print(i++ + ". ");
    System.out.println(snapshot);
    if (i == 20) break;
}

```       
        
```json        
0. {"symbol":"URE","sentiment":0.125,"variance":9500}
1. {"symbol":"WEATHER-SOYBEANS","sentiment":0.2,"variance":4327}
2. {"symbol":"BEAM","sentiment":0.6723163842,"variance":19246}
``` 



##### `order`
    You can use the order parameter to return the data sorted by a field, for example:

 * `variance`  Returns the data in ascending order
 * `-variance` Returns the data in descending order



```java   
for (Object snapshot : new Snapshots().variance(3000).fields("variance", "sentiment").order("-sentiment")) {
	System.out.print(i++ + ". ");
	System.out.println(snapshot);
	if (i == 20) break;
}
```       
        
```json        
0. {"symbol":"BEAM","sentiment":0.7006802721,"variance":15967}
1. {"symbol":"WEATHER-SOYBEANS","sentiment":0.2,"variance":4327}
2. {"symbol":"URE","sentiment":0.1,"variance":5900}
``` 

## Replacing `json-simple-1.1.1.jar`.

1.  Override  `protected Object parse(BufferedReader br)` to call your new JSON parser.
2.  Override `protected int resultsSize()` to return the size of the JSON result array.
3.  Override `protected Object resultsGet(int index)` to return an element of the JSON result array.
4.  Override `protected Object responseGet(String key)` to return an value of the JSON response object.



