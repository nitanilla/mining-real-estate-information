#Flatfinder helps you to find a flat.

If you have ever tried to find a decent apartment in a popular city like Berlin, you know that you have to be quick. Very quick. When there is a new ad you have to make contact within a few minutes, if you want to get an invitation to visit the advertised flat.

Flatfinder checks the real estate websites of your choice once or twice a minute and notifies you via email or iOS push message, as soon as it finds a new ad. You don't have to sit in front of your computer to find a flat, let Flatfinder do this for you! 

This script helped me to find my awesome flat, so it can help you to! 

Please note, you should see this project more as a starting point for your own script. I doubt that mine will work out of the box for you.

## Configuration
You need:

1. A server to run this script 24/7. Or an old computer that is always on.
2. A new email address. You will get a lot of messages (up to hundreds of mails a day), so do yourself a favour and get a special mail account for this. Also you need to know the SMTP settings.
3. Specific URLs of the real estate websites (more about this later on)
4. Optional: A Prowl account to receive iOS messages

Edit the configuration file to enter all the details.

### Supported websites
Currently this script supports these german websites:

* WG-Gesucht (1-Zimmer Wohnung)
* WG-Gesucht
* Immowelt
* ImmobilienScout24
* Immonet
* eBay Kleinanzeigen
* Wohnungsboerse

Take the URL from the example configuration file and visit the website. Now change the filter etc. to your needs, but make sure that the layout stays **exactly** the same. Otherwise the script will not be able to find any ads. Then copy/paste your own URL into your config file.

### Create your own signature
If you want this script to support your website of choice, first edit *Configuration.py* and your configuration file. Make sure you add it to the *self.URLs* dictionary.

The more difficult part is fetching the needed information from the HTML code of the requested website. Add a function to *WebsiteParser.py*, that returns the title, link, rent, location and the request time of the newly found ad. You can use an HTML parser like BeautifulSoup to do this or an regex.
