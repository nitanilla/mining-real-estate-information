##Broker Bot
Broker Bot (aka Houselistings), is a simple Rails app that keeps track of property listings as they are discussed via email between real estate broker and buyer.   While it was born out of a real world problem to replace manual list making via spreadsheets with an automated process, it's true purpose is to gain experience with Nokogiri (scraping), Resque (background processes), and Postmark (inbound and outbound email parsing).  

It is deployed via Heroku's Cedar Stack.

*How it Works*

###Email Parsing via Postmark<br>
A copy of any email exchanged between broker and client is sent to a mailbox at [Postmark](http://postmarkapp.com/).  Postmark does the hard work of receiving and parsing the inbound email and squirting it back out to Broker Bot as nicely formatted JSON data.   Postmark POSTs this data to a Broker Bot url, which in turn scans the body of the email for any URLs which may be URLs that contain a real estate property that is for sale.  Broker Bot creates a new record for each valid URL it finds in the email body.

###Page Scraping with Nokogiri and Resque<br>
For each valid URL that connects to a real estate listing website (be it Corcoran, StreetEasy, Trulia, etc), Broker Bot spins up a background process managed by the amazing Resque.  The background process uses Nokogiri to fetch (scrape) relevant data about the listing, including price, address, time on market, description, and photos.  This data is added into the record of the listing on Broker Bot.

###Display via the DataTables plugin for jQuery<br>
The data is eventually displayed to the user via the awesome and powerful DataTables plugin for jQuery.  DataTables provides the ability to sort and search the index level view (much as one would do with a Spreadsheet).


