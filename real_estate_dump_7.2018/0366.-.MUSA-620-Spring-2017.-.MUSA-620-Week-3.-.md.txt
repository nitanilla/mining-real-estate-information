# MUSA620-Week-3
Web Scraping ([notes](https://github.com/MUSA-620-Fall-2017/MUSA-620-Week-3/blob/master/week-3-web-scraping.pptx))


# Assignment

This is the first required assignment of the course. You may turn it in by email (galkamaxd at gmail) or in person at class.

**Due:** by the end of class next week, 8-Feb

**Task:** Calculate the price per square foot of condominiums on Rittenhouse Square (the orange buildings below) by scraping the Philadelphia Property Database.

![Rittenhouse Square](https://blueshift.io/rittenhouse.png "Rittenhouse Square Condominiums")

**Deliverable:** The average price per square foot based on your calculations. Please also include all R scripts used in scraping and analyzing the data, as well as information about any other tools / applications used outside of R.

To calculate the average price per square foot for these homes, you will need to scrape the [Philadelphia Property Database](http://property.phila.gov/).
- This list of condos (address and unit #) are in the [rittenhouse-condos.csv](https://github.com/MUSA-620-Fall-2017/MUSA-620-Week-3/blob/master/rittenhouse-condos.csv) file. See the [assignment-week-3-template.R](https://github.com/MUSA-620-Fall-2017/MUSA-620-Week-3/blob/master/assignment-week-3-template.R) script for some code to get you started.
- For the purposes of this assignment, please use the most recent Market Value as the price of the condo, as shown in the "VALUATION HISTORY" table. For the area of the condo, please use the field labeled "IMPROVEMENT AREA (SQFT)".
- This assignment may require you to go beyond the examples we covered in class, though the [nyc-real-estate-search.r](https://github.com/MUSA-620-Fall-2017/MUSA-620-Week-3/blob/master/nyc-real-estate-search.r) script should include most of the pieces that you need. I also added some additional information about selectors into the [lecture notes](https://github.com/MUSA-620-Fall-2017/MUSA-620-Week-3/blob/master/week-3-web-scraping.pptx).
- **UPDATE<a name="update"></a>: For this project you should use [Selenium](https://cran.r-project.org/web/packages/RSelenium/RSelenium.pdf), rather than Rvest, to extract data from the page. There is a bug in some versions of Firefox that will give an error when you try to extract the HTML and hand it off to Rvest.**

**Setting up the Selenium Standalone Server (optional):**
- 1. Install Java JDK, following [these intructions for Windows](https://docs.oracle.com/javase/8/docs/technotes/guides/install/windows_jdk_install.html) or [these instructions for OS X](https://docs.oracle.com/javase/8/docs/technotes/guides/install/mac_jdk.html). You can download the latest Java JDK version [here](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
- 2. Download the latest version of the [Selenium Standalone Server](http://www.seleniumhq.org/download/).
- 3. If you do not already have it, install the latest version of [Firefox](https://www.mozilla.org/en-US/firefox/products/) (Firefox is the default browser for Selenium).
- 4. To start the server, open the command line (in Windows press Win+R then type "cmd", in OS X search for "terminal" in Spotlight). Go to the directory where the Selenium Standalone Server file is downloaded and run "java -jar selenium-server-standalone-3.0.1.jar".


If you are having problems getting the Selenium Standalone Server working, you can find more [information here](https://cran.r-project.org/web/packages/RSelenium/vignettes/RSelenium-basics.html). You are also welcome to email me with questions. However, this project is not meant to be an exercise in setting up servers, so if you are finding it overwhelming to set up the standalone server, you should just use [Sauce Labs](https://saucelabs.com/), as we did in class. You can sign up for a [free Sauce Labs trial account here](https://saucelabs.com/signup/trial).

**Office Hours:**
Office hours are on Monday, 1pm to 5pm. Email me at galkamaxd at gmail to set schedule a time to discuss the project. You are also welcome to email me with questions at any time.
