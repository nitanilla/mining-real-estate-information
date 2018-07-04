# Brokerhub 1.0

## About

BrokerHub 1.0 is proprietary prototype Commercial Real Estate listing database designed to be implemented on Brokerage Firm's website as a plugin. The application comes in two parts: a desktop node application that can parse Microsoft Excel files and insert them into a backend SQL Database, and a front-end that can be inserted onto a Commercial Real Estate Website.

The plugin is designed to augment a firm's research department and listing services so that they can display live data about multiple Markets, Product Types, and Submarkets automatically, rather than rely on conventional Market Research Reports, which can take weeks to create.

![brokerhubscreenshot](github/brokerhub.png)

### View Listings in Map
![brokerhubscreenshot](github/brokerhub1.png)

Shows detail on Map using API Plugin.

### Manage User Account Information
![brokerhubscreenshot](github/brokerhub2.png)

Example charts. Charts can be modified and styled as needed.

### Backend Spreadsheet Parser (Desktop Application)
![brokerhubscreenshot](github/brokerhub4.png)

The Desktop Node application parses sample Excel Spreadsheets using the ExcelJs npm package, and then connects the data to the Database hosting on MySQL.

### Backend SQL Database
![brokerhubscreenshot](github/brokerhub3.png)

The backend SQL database that the Application pulls its data from.


## Motivation

Most Research Departments at Commercial Real Estate firms rely on static pdf documents to display their research data. Additionally, the creation of market reports can be very labor intensive and involves manually parsing hundreds of Excel sheets. Having a parser that can sort through and organize those sheets would save dozens of manhours each quarter. Additionally, by inserting this data into an SQL server, which can then be called through an API to a Front End application, this data can be utilized in additional ways that add value to a firm.

## Authors

Kevin De Bree (@kpdebree)


## License

MIT License
