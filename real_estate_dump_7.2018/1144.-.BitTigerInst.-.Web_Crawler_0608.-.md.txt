# 0608-Web-Crawler

## Description

This project is ultilizing Scrapy to crawl and scrape a web page (http://www.trulia.com). The content crawled will be saved in MongoDB and display on our pages sorted by diferent feature like ranking and number of times read. This crawler collects the mortgage dataset from trulia website and we will develop a web application to display the mortgage for sale based on the zip code. We also apply some filters such as house's prices and condition to enhance user experience.


 we can start with NJ, because it is a small state and divided into 3 area, north jersey, central jersey, south jersey. then we can get a list of all counties and zip code or area under each county. Then we can crawl the Trulia website for 
 (1) summary page of median price, school rating, demographics 
  http://www.trulia.com/real_estate/Millburn-New_Jersey/
  (2) list  of houses for sale and their basic information, and store on our data base
 http://www.trulia.com/for_sale/Millburn,NJ/list_v/
 
 in the mean time we can search for a table of distance  between zip codes in NJ, so we can implement the radius in search
 
 the final product will have the following function: user (1) select north/ south/mid NJ (2) input median house price/budege and sqft/ rent price,   school rate,  other demographics (3) get results of zip codes and a list of summaries for that zip code (4)  see the listings in this zip code and further filter by bedroom number/bathroom number etc
 
 if we get the distance between zip codes, we can replace (1) with a center zipcode and a selection of radius 10 miles, 20 miles 30 miles etc.  
 
## Plan
- 1) Analyze trulia's website to create data model for the project.
- 2) Create a web crawler project and implement function requirements to generate the mortgage database.
- 3) Integrate MongoDB with the web crawler to store all collected data.
- 4) Build backend web services using Express JS.
- 5) Develop frontend using Javascript, Bootstrap, and HTML5. 

##Bonus (when having extra time)
We like to collect and display the monthly rent estimate data from [Zillow](http://www.zillow.com). This feature can help users gain more vision and have better decision making before purchasing the property.

### Todo List

- [ ] Create a scrapy project to craw data from specified url.
- [ ] Save the crawled data in MongoDB.
- [ ] Display and sort data by diferent features.

### Time Schedule

| Stage | Start  | End | Goals |
| ------------- | ------------- | ------------- | ------------- |
| 1 | 08/29/16  | 09/04/16  | Project Selection, Plan Discussion, and Proposal Draft Writing |
| 2 | 09/05/16  | 09/11/16  | Enviroment Setup | 
| 3 | 09/12/16  | 09/18/16  | System Desgin |
| 4 | 09/19/16  | 09/25/16  | Implement crawling function, crawl list page and detail pages |
| 5 | 09/26/16  | 10/02/16  | MongoDB Setup and Saving data |
| 6 | 10/03/16  | 10/09/16  | UI Feature and Presentation and Document Making |

## Resource
- [BitTiger Project: AppStore - Crawler](https://slack-files.com/T0GUEMKEZ-F0J4G9QTT-274d3bc97e)
- [BitTiger Resource](https://bittigerinst.github.io/web_crawler)
- [MongoDB](https://www.mongodb.com/)
- [Data Source](http://www.trulia.com/)
- [Setup Enviroment](https://docs.google.com/document/d/1ykSQo-IbPnCFTZOufhNsz-2oYXxjyCknIo6SABjD2Rg/edit?usp=sharing)
- [Setup Backend Environment](https://docs.google.com/document/d/1g4ouNfkfN5JsqZeW1ttZNCEC_Qf0QsQ42wRt5GJ8_kY/edit?usp=sharing) 

## License
See the [LICENSE](LICENSE.md) file for license rights and limitations (MIT).

## Project Information
- category: full stack, web crawler, web application
- team: Coming soon
- description: Web Scrapy to craw valuable resource
- stack: Python, Mongodb, JavaScript, XPath, Scrapy, Express JS, Bootstrap


