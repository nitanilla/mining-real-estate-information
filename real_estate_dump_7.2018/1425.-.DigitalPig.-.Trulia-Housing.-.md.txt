# Trulia-Housing
Smart Househunter / Smart House Seller

This project is to answer the question: Is there a *best* time for buyer to buy
a house in a year? Does the house hunting process affected by weather? The
question is inspired by my experience of purchasing a house before. During the
process, my realtor gives me a few of “old man's wisdom”. For example, the
market has more listings in the summer time that those in winter. Also, if the weather is good, there are more buyers out to look for houses. This small project is to grab the real estate data from website like Trulia and use that as the source to validate those “wisdoms”.

The data is scrapped from Trulia via its API. The script is written in
Python3. You have grab your own key before you start. Just go to
[Trulia API](http://developer.trulia.com). They have a few of API returning
average listing price, median listing price, amount of online traffic to Trulia
for each neighborhood, city or state. The weather data can be downloaded from National Oceanic and Atmosphere Administration (NOAA). All data was then combined and processed by R for post-analysis and plotting.

The conclusions are:

![state-time](https://github.com/DigitalPig/Trulia-Housing/blob/master/state-time.png)
1. Not all states show this “more houses in summer” rule. From graph1, there are
   even more listing on the market during the winter time of 2013 and 2014 in
   Florida. But most states, the wisdom is somehow valid. However, in the big
   picture, number of listings is more affected by the economy (as you can think
   of...). In 2011 and 2012, number of listing is keep going down, as the job
   market is going back to normal.

![price-time](https://github.com/DigitalPig/Trulia-Housing/blob/master/price-time-state.png)
2. In graph2 (not shown but you can see on GitHub) is the price to time
   graph. Surprisingly, other than DC and CA, most states has flat
   curve. Anyway, one did not see any seasonal effect in the price by time. So
   at this point, we can make the conclusion that if you live in those states,
   your best time as a buyer probably is still summer time, when you would see
   more housing but same price.
   
![temp-traffic](https://github.com/DigitalPig/Trulia-Housing/blob/master/temp-traffic.gif)
3. The next graph shows you the overlay of temperature and Internet traffic to
   Trulia in CA in 2013. Temperature is plotted as a square with the measuring
   station coordination as the center in unit degree C. The online traffic to
   each city in CA is plotted as dot with scaled size related to the amount of
   traffic. You can see that the online traffic has no effect to temperature
   changes. This is understandable because you probably stay at home comfortably
   while surfing Trulia when the outside is 110F. :) Anyhow, it tells us that no
   matter how hot the outside is, people just have constant interest looking at
   the house market on line.

The further improvement that I want to do if I have more time is to grab the
real transaction data from Trulia/Zillow/County auditor website to have a better
idea about the real market activities.

Hope you enjoy the project. Check back regularly as I will keep these code updated!


