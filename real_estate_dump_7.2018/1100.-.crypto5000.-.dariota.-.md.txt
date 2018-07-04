# Dariota: Decentralized Augmented Reality using IOTA

Dariota has launched a beta version at https://dariota.com. The key insight:

> Latitude and longitude geo-coordinates can be deterministically mapped to IOTA addressses.

This implies that you can connect a GPS system (a smartphone/etc) to the IOTA Tangle and use the IOTA data layer to map elements to locations. So imagine having an augmented reality data layer using IOTA at every location on Earth.

Use cases:
* Virtual tours: you can pin facts to a location or read about facts at a location. Facts are stored in the Tangle and display based on lat/long coordinates.
* Messages/chat: you can leave messages as data for people at locations. People can read messages at locations.
* Decentralized yelp: you can leave reviews for businesses at locations. You can read reviews at locations.
* Games: think Pokemon Go, but with IOTA. Treasure hunts at locations. 
* Real Estate Info: housing prices, construction data, occupancy stats, etc.
* Traffic or Incident Info: cars or passengers can post traffic accident data or construction delays
* Location-Based Advertising: you can advertise your business or special deals available at a time point
* Yard Sales: you sell individual items at a point location
* Airbnb reviews: you can leave reviews of airbnb hosts

## Writing Data Demo
![Write Demo](/img/writedemo.gif)

## Reading Data Demo
![Read Demo](/img/readdemo.gif)

## Payment and Accounts
Get paid for your data by attaching a payment account. For example, post a traffic accident and people can pay for your helpful data. Accounts are optional and guard against IOTA address reuse. If you don't want an account, you can still include a payment address.

## Storage * 
(Experimental). You can pay to have any posted data stored for a certain time period to prevent snapshot deletion.

## Filters
When reading data, you can filter the displayed results by factors like geographic radius, message type, and time expiration. Posted data can be upvoted. This provides another measure of quality and a possible future filtering criteria.

## Replies
You can view replies to a posted data point. This is particularly important for chat messages or questions.

## Dariota Format
Each Dariota Transaction has 3 key elements: Address, Payload, Tag

The Dariota Address is a deterministic conversion of a latitude-longitude combination converted into an IOTA address. The lat-lon coordinate is at 1 decimal precision.

```javascript
let latitude = "LAT_VAL_FROM_GPS";
let longitude = "LON_VAL_FROM_GPS";

// convert latitude and longitude to just 1 decimal - parse off from string
let tempPos1 = latitude.indexOf("\.");
let tempPos2 = longitude.indexOf("\.");
let tempString1 = latitude.substring(0, tempPos1 + 2);
let tempString2 = longitude.substring(0, tempPos2 + 2);
let locationAddress = tempString1 + " " + tempString2;

// perform Dariota mapping
locationAddress = locationAddress.replace(/0/g, "A");
locationAddress = locationAddress.replace(/1/g, "B");
locationAddress = locationAddress.replace(/2/g, "C");
locationAddress = locationAddress.replace(/3/g, "D");
locationAddress = locationAddress.replace(/4/g, "E");
locationAddress = locationAddress.replace(/5/g, "F");
locationAddress = locationAddress.replace(/6/g, "G");
locationAddress = locationAddress.replace(/7/g, "H");
locationAddress = locationAddress.replace(/8/g, "I");
locationAddress = locationAddress.replace(/9/g, "J");
locationAddress = locationAddress.replace(/\./g, "K");
locationAddress = locationAddress.replace(/\-/g, "L");
locationAddress = locationAddress.replace(/\+/g, "M");
locationAddress = locationAddress.replace(/\ /g, "N");

// perform Dariota mapping - pad the address to the proper length
let tempLength = locationAddress.length;
let padLength = 81 - tempLength;
let i = 0;
while (i < padLength) {
     locationAddress = locationAddress + "Z";
     i++;
}
```

Each read of Dariota is at the 1 decimal precision range. Once a read has been queried, there are 5 precision ranges for filtering using decimals 1 to 5. For example, you can filter matches for XX.XX at the 2nd decimal level.

The Dariota Payload uses a vertical lined spaced format. The type is a 4 letter identifier (e.g. CHAT,ITEM,SERV,REVI). The latitude and longitude are full precision coordinates (not filtered at 1 decimal). The data expiration is formatted mm-dd-yyyy. The dataAccount is a 27 character account to identify payment addresses. The dataAccount is overridden with a payment address (dataAddress) if available. Finally, the dataText is just the standard message created by the user.

```javascript
// create the message payload format
let message = dataType + "|" + latitude + " " + longitude + "|" + dataExpiration + "|" + dataAccount + "|" + dataAddress + "|" + dataText;        
```

The Tag is just a 27 unique identifier used for replies and voting.
