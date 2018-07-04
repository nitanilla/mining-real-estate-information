# Josh's Real Estate Web Scraper

Easily scrape real estate web data from https://www.realtor.com/

A browser automation script with nightmare.js that navigates to a page and exports data to a .csv file for easy manipulation. 


# Usage

## 1. Clone this repo
 
```
git clone https://github.com/jchianelli7/RealtyScraper.git 
```

## 2. Node Install
Go to the Node.js Downloads page [https://nodejs.org/en/download/]
Download Node.js for your system
Run the downloaded Node.js .pkg Installer
Run the installer, including accepting the license, selecting the destination, and authenticating for the install.
You're finished! To ensure Node.js has been installed, run 
```
node -v
```
 in your terminal - you should get something like v6.9.4


## Run Nightmare Realty Scraper

```
node realty.js
```
which by default selects the zipcode "53217" (Milwaukee, WI) or
```
node realty.js (5 Digit zipcode)
E.g.    node realty.js 90210
        node realty.js 60007
        node realty.js 10001
```
to collect real estate data for other zip codes


## Use It

You should use this scraper and make a similar one that scrapes what you want (feel free to open issues and ask questions!).

It's a scraper that can scrape as often as you like and can scrape virtually any location. Works only on https://www.realtor.com/
