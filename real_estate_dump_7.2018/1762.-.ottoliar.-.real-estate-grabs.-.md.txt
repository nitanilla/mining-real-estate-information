These are a series of scripts made for a real estate broker.  He told me that he had some sort of contract with his buyers that if he could notify them of a listing first, he would get the commission over other agents who notified the buyer at a later date.

These scripts use [Selenium-WebDriver](https://github.com/SeleniumHQ/selenium/tree/master/javascript/node/selenium-webdriver) in order to navigate to various real estate websites at regular intervals.  The scripts pull all of the listings on the page and their relevant data, and compare them to listings in MongoDB (using [PyMongo](https://github.com/mongodb/mongo-python-driver)).  
If the listing is not found in the database, it is immediately emailed out to the broker before being inserted into the database.

