# Philadelphia Real Estate Tax Downloader

![Philadelphia Real Estate](/demo/pictures/PhillyLogo.png "Philadelphia Real Estate")

This is a tool to be used to gather tax information on specified real estate within the state of Philadelphia.

It uses peewee and SQLite for data management; Selenium via Chrome for headless browsing, and xlrd and xlwt 
for outputting the data to CSV and Excel.

Utilizing Selenium, the script has five steps: 

- Parse a list of addresses whose information need to be downloaded
- Navigate to Philadelphia's .gov real estate site, specifically the address search page
- Input each address into the search bar and parse out the specified addresses' tax information
- Temporarily store data in an SQL database
- Output all gathered data to an Excel spreadsheet
* Additionally, output any errors from failed address lookups

Every page parsed using Selenium is downloaded and saved to a database via SQLite for safe-keeping,
and the script should restart the browser automatically to forgo any crawling protection.

Data is parsed by the script via a pre-defined list of addresses within a CSV file. The CSV file must have each
address to be parsed in the A (or first) column of the spreadsheet to be read by the script. There is no limit
to the amount of addresses that can be added.

Any address that has a problem while downloading will be output to an Error file with a message explaining the issue.

This project utilizes two other projects of mine: [python-utilities](https://github.com/kelmore5/python-utilities) and [SeleniumBrowser](https://github.com/kelmore5/SeleniumBrowser), both of which
should already be uploaded within this git repository.

*Note: SQLite was chosen over MySQL or Postgres to improve portability of the script, but any database could be 
adopted if need be.

This has been checked and was working on **May 22, 2018**, but I have no plans to maintain the project.

## Install

### Dependencies

- python 3.6
- xlrd
- xlwt
- [selenium](http://selenium-python.readthedocs.io/installation.html)
- [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/)
- [peewee](https://github.com/coleifer/peewee)

### Run

First, download the repo

    git clone --recurse-submodules -j8 https://github.com/kelmore5/philly-real-estate-parser
    
Once downloaded and dependencies are installed, you can run it via

    python3.6 lib/PhillyParser.py

## Similar Projects

- [Ebay Keyword Crawler](https://github.com/kelmore5/ebay-keyword-crawler)
- [Masonic Web Parser](https://github.com/kelmore5/masonic-web-parser)

## Extra Links

- [Selenium](https://www.seleniumhq.org/)
- [Selenium Python Docs](http://selenium-python.readthedocs.io/)
- [Peewee Documentation](http://docs.peewee-orm.com/en/latest/)

## Proof of Concept

You can see a demo from a slideshow I've created [here](https://docs.google.com/presentation/d/1VPjsRnpOAuN5QHK1tTbLZbcRY8SmyyCg2Wh8LCeIB-Y/present)
or you can look at the sample output from [this](https://github.com/kelmore5/philly-real-estate-parser/raw/master/demo/Estates_2018-05-22%2018:48:30.xlsx) Excel sheet, screenshotted below.

Either way here are some pictures to give a proof of concept (Note: All address information has been voided to protect client data).

Input the CSV file with predefined addresses to parse

![CSV Input](/demo/pictures/ScriptStart.png "CSV Input")

Navigate to Philadelphia’s real estate search page

![Philadelphia Search Page](/demo/pictures/AddressSearch.png "Philadelphia Search Page")

What the search results look like for each property

![Search Results](/demo/pictures/PropertyInformation.png "Search Results")

An example of the script running 

![Script Running](/demo/pictures/ScriptRunning.png "Script Running")

All property information has been input into an SQL database

![Properties Database](/demo/pictures/PropertiesDatabase.png "Properties Database")

All tax information has also been input into an SQL database

![Taxes Database](/demo/pictures/TaxesDatabase.png "Taxes Database")

Script wrapping up and outputting data to Excel

![Script Finished](/demo/pictures/ScriptFinished.png "Script Finished")

Output everything to Excel:

![Excel Output 1](/demo/pictures/ExcelOutput_1.png "Excel Output 1")

![Excel Output 2](/demo/pictures/ExcelOutput_2.png "Excel Output 2")
