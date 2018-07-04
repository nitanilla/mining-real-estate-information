Wrapper for the EveryBlock API
===============================

Built by Harper Reed ([harper@nata2.org](mailto:harper@nata2.org)) - [@harper](http://twitter.com/harper)    
[git@github.com:harperreed/simple-everyblock.git](https://github.com/harperreed/simple-everyblock)    
You can get an API key here: [https://chicago.everyblock.com/api-signup/](https://chicago.everyblock.com/api-signup/)    
Documentation is here: [http://www.everyblock.com/apidocs/](http://www.everyblock.com/apidocs/)    
Google Group is here: [http://groups.google.com/group/everyblock-api/](http://groups.google.com/group/everyblock-api/)    

Notes:
-----

For some reason I found this API a pain in the ass to deal with. One of the reasons I built this class is to make it super easy. 

Hopefully this will help some people consume the data.

I used beutiful soup to handle the XML so it could be used in places that lxml and the like cannot be used (App Engine).

*`<small_rant>`*

A couple things have bothered me about this API since I started playing with it. I figured I would put them here. 

 * WTF are Schemas? They seem to complicate things.

 * WTF @ xml. This isn't 1998. Most people are going to want this data as an object, so why not use JSON or some other machine serializable data format. If XML is important, then have it be an option. If XML is the only option, then treat it like xml: have DTDs and use Namespaces. 

 * Why only 24 hrs of data? You are creating a relationship here the API consumers will have to cache and store all of *your* data, because it is impossible to get at the data past 24hrs. You lose control of your data.

 * Where is my API key? If you lose it, you have to get another one. I wish it were associated with my EB account. 

This API seems built to dissuade people from using the EB data. Why is it so hard to figure out? I have dealt with a few apis and I still don't understand exactly whats going on with this API.

However, once you deal with the annoyance and you get the data - it is awesome

*`</small_rant>`*

Usage:
------

    >>> from simple_everyblock import simple_everyblock  
    >>> api = simple_everyblock(api_key=api_key)  
    >>> print api.get_metros()  
    [{'city': u'Atlanta', 'state': u'GA',...............  
    >>> print api.get_schemas('dc')[0]  
    {'url': u'http://dc.everyblock.com/commercial-real-estate/', ...............  
    >>> print api.get_location_types('dc')  
    [{'url': u'http://dc.everyblock.com/locatim.................  
    >>> print api.get_locations('dc','neighborhoods')  
    [{'url': u'http://dc.everyblock.com/locations/neighborhoods/bolling-air-force.......  
    >>> print api.get_newsitems('dc', '2010-01-06-1900', '11')

Should be simple
