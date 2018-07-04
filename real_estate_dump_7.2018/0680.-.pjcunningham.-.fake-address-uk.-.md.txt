fake-address-uk
===============

Generates randomized UK addresses using real UK data (Towns, Counties, Post Codes etc). 

```C#

    public class FakeAddress {

        public string Address { get; set; }
        public string BuildingName { get; set; }
        public string Number { get; set; }
        public string Street { get; set; }
        public string Suburb { get; set; }
        public string Town { get; set; }
        public string County { get; set; }
        public string PostCode { get; set; }
    }
```

How to use
---

```C#

	var addresses = FakeAddressGenerator.Generate(1000000);
	foreach (var address in addresses) {
		// do something with address
	}
```

If you don't need all the model properties just do a projection :

```C# var addresses = FakeAddressGenerator.Generate(1000000).Select(q => new {PostCode = q.PostCode});```
           
Sample Output
---

| Address | BuildingName | Number | Street | Suburb | Town | County | Post Code |
| ------------- | ------------- |------------- |------------- | ------------- |------------- |------------- | ------------- |
|Ground Floor, Offices 5/6|Lancer House|396/298|Wrexham Springs|Primrose Hill|Boltongate|Flintshire|N10 2QR|
|Morston Point|Old Marsh Farm|1058/1058A/1060|East Point Industrial Estate|Ballsbridge|Quorn|North Humberside|CF83 3NL|
|Unit 101/112|Ferry Works|LE1|Broadway Mall|Turnpike|Danbury|Isle Of Wight|W1U 3QA|
|Attleborough Fields Business Park|Building 12|2.23|Holme Court|Haybrook|Pucklechurch|Highlands|EC2R 6BH|
|Post Office|Swedenborg House|122a|Genesis Centre|West Norwood|Cwmbach|Bedfordshire|NG1 2BH|
|1st Floor (2)|Capital Place|457/463|Ephraim Street|Rattray|East Chaldon|Isle Of Lewis|NG5 6HA|
|1st Floor (Suite A)|Burges Place|FSU1|Main Road|Uppermill|Littleport|Isle Of Man|BT82 8AG|
|Warth Park|Mulberry Place|L79|Lewisham Centre|Thornton Heath|Sutton Weaver|Clwyd|ST6 2JW|
|Burgess Industrial Park|Spear House|63 &amp; 69|Cricketers Lane|Postling|Edinburgh|Dorset|OL8 1EU|
|Riverdene Business Park|Rathbone House|32a/33a|Crossley Road|Trecenydd|Thorpe Bay|Hampshire|BS16 3JB|
|Frenbury Estate|Westec|308|Golden Ball Street|Govan|London Sw13|Nottinghamshire|CF5 6EH|
|1st Floor Suite 4/5|Schwartz House|13B|Toat Hill Garage|Pilsworth|Creswell|West Glamorgan|S40 1SA|
|Units 22/25|Crown Mews|22/25|Lysander Close|High Heaton|Sandwich|Highlands|SA11 1DU|
|Eastfield Industrial Estate|Birch Close Farm|CC04|Capsie Drive|How Wood|Trevethin|West Midlands|EN11|
|Ground Floor Suite 352|Midland Bank Chambers|LSU2|Penny Lane|Undercliffe|Sturry|Fife|RH10 7AS|
|Pilgrim Suite|Whittington House|725/727A|Widnes|Bishopsgate|Harby|Cumbria|L7 4JG|
|Stafford Park 2|Rutland Studios|23U|Norman Court|North Ormesby|Sturminster Newton|Nottinghamshire|NG1 3AA|
|Montague Works|Rawlinson House|12/124|Dabies Road|Shard End|London W2|Nottinghamshire|BS1 3BF|
|Suite 2/2|The Cloisters|4255|Bianca Road|Frensham|Dovenby|Strathclyde|BH15 1AR|
