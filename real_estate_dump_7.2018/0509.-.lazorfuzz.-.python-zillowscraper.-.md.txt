# zillowscraper
![MIT License](https://img.shields.io/github/license/mashape/apistatus.svg)
[![Python 2.6|2.7](https://img.shields.io/badge/python-2.6|2.7-yellow.svg)](https://www.python.org/)
##### Multi-threaded Zillow scraper that retrieves and parses all agents in a given state.
Note: zillowscraper is an educational tool that demonstrates how one might retrieve real-estate agents from Zillow. This tool only saves the information of a Zillow agent when an email address can be located on their personal website.  The rest are discarded.<br>
#### Usage Example:
-
Getting agents in California
```console
python zillow.py California
```
Agents are saved in <zip code>.xlxs for each zip code in the state. This tool can be closed and restarted, and scraping will resume on the last zip code.<br>

-
#### Example output in an xlxs file:
```
Maria Casas	Buyer Seller	Coldwell Banker Beachside	"19671 Beach Blvd
Huntington Beach, CA 92648"	(xxx) xxx-xxxx	Mxxxxxxx@Coldwellbanker.com		
Michael Henderson	Seller	Keller Williams 	"16820 Ventura Blvd.
Encino, CA 91436"	(xxx) xxx-xxxx	mxxxx@myagentmichael.com		
Maribel Munoz	Buyer Seller	RE/MAX 	"Los Angeles 
Los Angeles, CA 90032"	(xxx) xxx-xxxx	Mxxxxxxxxxxxs@gmail.com		
Michelle T. Crane	Buyer Seller	Crane & Co Realty International	"11812 San Vicente Blvd Ste 100
Los Angeles, CA 90049"	(xxx) xxx-xxxx	xxxxxxxxx@xxxxxxxx.com		
Michelle Rivera	Buyer Seller	Z Realty	"10918 Hesperia Rd. Suite A1
Hesperia, CA 92345"	(xxx) xxx-xxxx	hxxxxx@yahoo.com		
Nick Astrupgaard	Buyer Seller	Brock Real Estate	"2235 Hyperion Ave
Los Angeles, CA 90027"	(xxx) xxx-xxxx	nxxxxxxxxxx@gmail.com		
Natalya Shcherbatyuk	Buyer Seller	Champion Realty	"1701 Truman St. #1
Los Angeles, CA 91340"	(xxx) xxx-xxxx	nxxxxx@championrealty4u.com		
Ryan Shaw	Buyer Seller	Teles Properties	"129 Gull St.
Manhattan Beach, CA 90266"	(xxx) xxx-xxxx	rxxxxxw@telesproperties.com			
```
-
#### Dependencies
zillowscraper uses the BeautifulSoup module. To install BeautifulSoup in command line via pip:
```console
pip install beautifulsoup4
```
