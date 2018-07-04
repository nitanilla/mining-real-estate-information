Rubeclosures - Ruby API wrapper for the foreclosurelistings.com API
----------------------------------------------------------------------------------
The Real Estate industry has some incredibly annoying technology habits, so imagine
my surprise when I saw that foreclosurelistings.com had finally implemented an API!

Rubeclosures is just a simple Ruby wrapper around their API. Nobody likes parsing XML
(even in Ruby, admit it), so what Rubeclosures does is wrap their data into native
Ruby objects for your convenience.


Documentation
----------------------------------------------------------------------------------
Using Rubeclosures is pretty straightfoward. Just consider the following code...

    require 'rubeclosures'
    
	# Pull down up to 10 of the most recent foreclosure listings in your area
    
	# Get your api_key at foreclosurelistings.com
    lol = Rubeclosures.new("domain", "api_key")
    
	# Pass in state/area/county, or zipcode (object-ified)
    epic = lol.getRecent({:zipcode => "20910"})
    
    puts epic[0]["city"]

You can also pass Rubeclosures an existing address to check if it is a foreclosure or not.

    require 'rubeclosures'
    
    lol = Rubeclosures.new("domain", "api_key")
    
	# Check if this is a foreclosure or not (address/city/state as straight up args, non-obj)
    epic = lol.getRecent("12345 Sesame St", "everytown", "CA")
    
	# Same data-style is returned; if the API is working correctly, you may have a string message
	# to check against.
    puts epic[0]["city"]


Questions, comments?
----------------------------------------------------------------------------------
Hit me up at (ryan [at] venodesigns [dot] net), or on Twitter - http://twitter.com/ryanmcgrath
