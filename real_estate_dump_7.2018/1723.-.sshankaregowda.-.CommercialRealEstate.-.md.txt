# Commercial Real Estate
Getting Started - quick user guide.
  1.  Clone the code  
  2.  Execute the mvn command to run
  3.  I have built and tested on MAC OS
 
Test overview -
 Commercial Real Estate page is launched
 Clicks on property, franchise, business for sale and news tab
 Verification is done to check if pages are loaded successfully

 
Framework Overview -
1. TestNG Framework
  This module contains reusable user actions built using Selenium Webdriver Java.It is built using maven
2. Page Objects
  This module contains all the functions specific to the application. This module contains different java classes which is specific to number of webpages in the application.
3. Runner
  This module contains runner class to execute the test cases.
4. Feature File
  This module contains test cases defined using BDD Cucumber Gherkin Language
5. Resource
  This module contains inputdatasheet and testng.xml which allows to do execution of test cases in batch as well as parallel execution.
  pom.xml contains all the dependencies and testng contains test suites
   
