# prime-group-project

This project can be found at: www.homesavants.com

Nate Labatt Realty
3/24/2015 | Version 0.0.1
Document Objectives
The purpose of this document is to provide detailed documentation to Nate Labatt & Eric Hermanson ("The Client") that clearly defines the work that Prime Students Andy Fehrenbach, Kati Lueth, Juan Ball, and Alex Minge ("The Company") will perform and the deliverables you will receive within the scope of this project. By accepting this document you acknowledge your understanding and agreement to this scope of work. Any requirement which falls outside the specifications in this document will be considered "Out of Scope" and may require reprioritization or removal of other features to implement.

This document takes precedence over any other documentation provided regarding scope of work.
Overview
The Company will produce an end-to-end web application for The Customer that will provide real estate and house-flipping investment analysis to registered users and user data to The Customer. The app will feature a real estate search by zip code, assumptions and analysis features, a mortgage calculator and a resources feature. The Client will be able to view select user data including name, email and phone number as well as manage the Resources page content. The Company will design the application to allow future extensibility, including the option of paid premium user accounts.
Workflow of Application
Users register for a new account or login. The application will use Passport Authentication to verify the user log-in and registration accounts. The registration feature will require a username, email, password, first and last name and (optionally) a phone number. 

If the user forgets his/her password they can use the password recovery feature that will send an email to the registered email address. The email will include instructions with a link that will take the user to the New Password View on the website. Clicking the link will reset the user’s password and allow them to submit a new password.









Figure 1.1 - Login Splash Page View 
Email/Username field
Password field
Login button
Register button

















Figure 1.2 -  Registration
First Name field
Last Name field 
Email field
Password field
Re-enter password
Phone Number field
Login button















Home View
Upon successful login users will see the Home View. The Home View is where users will be able to search for available properties by zip code. The house listings will be pulled from SimplyRETS.com API, which utilizes the information from the MLS credentials provided by The Client. When the user clicks the button to search by zip code a request to the API will be made. The API will return information including thumbnail images, square footage, total price, price per square foot, address, number of bedrooms, and number of bathrooms. This information will be displayed to the user in a Result Tile. The user will click on one of two buttons, ‘Evaluate’ or ‘Mortgage’ to take them to the appropriate application page.

Figure 2.1 - Home View

Search field
Search button
Result tiles
		























Figure 2.2 - Result Tile

Image thumbnail (if available)
Price per Square Foot
Square Feet
Address
Bed/Bath
Price
Evaluate page button (will go at bottom of tile)
Mortgage page button (will go at bottom of tile)










New Deal Analysis
The New Deal Analysis View will use the information from the selected Result Tile listing. The content of this view is modeled after the reference(www.rehabvaluator.com) supplied by The Client. The Assumptions panel (figure 3, item 1) will automatically populate with information about the selected listing. The user will push a button to run calculations to determine the profit / loss statistics for the given property that will be displayed in the Flip Panel and the Hold and Rent Analysis Panel.

The Assumptions Panel will feature hidden form fields that will be displayed when a “finance” button is checkmarked. The data gleaned from calculations in the assumptions panel will be used in the exit strategy panels. The Flip Panel (Exit Strategy #1) will be modeled after the supplied reference, www.rehabvaluator.com. The Hold and Rent Analysis Panel (Exit Strategy #2) will be modeled after the supplied reference www.rehabvaluator.com. After the Assumption Panel Button has been clicked Users will have the option to continue to the Mortgage Calculator via the Mortgage Calculator Button or be directed to the Home View via the ‘New Search’ button.






Figure 3.1  - New Deal Analysis View

‘Assumption Panel’ form 
Finance Checkbox
Submit Assumption Panel Button
‘Flip Analysis’ result panel
‘Hold and Rent Analysis’ result panel
Mortgage Calculator Button
New Search Button











Figure 3.2  - Assumptions Panel





















Figure 3.3  - Flip Analysis Pane (Exit Strategy 1)







































Figure 3.4  - Hold & Rent Analysis Pane (Exit Strategy 2)













Mortgage Calculator
The Company will build mortgage calculator that will include an industry standard equation of the monthly interest rate, total cost of the house and user selected monthly payments.

Figure 4 - Mortgage View

Selected Result Tile Image
Mortgage Calculator
Calculate Mortgage Button
Monthly Payments Dropdown


































Resources

The Resources View will contain PDF files that users of the site may download by clicking on the image thumbnail. The resources will be provided to the Company by the Client. The PDF files will be hosted using Amazon Web Services S3 (AWS S3) document hosting. The Client will be able to upload new and manage existing files via AWS S3. This page will also contain a link to The Client’s blog.  

Figure 5  - Resources View

Image Thumbnails
PDF title
PDF description
Link to the blog
































Admin Account
The Admin View will be available only to users that hold ‘Administrator’ status as determined by The Client. The Admin tab in the navigation bar will appear when an administrator logs in. The admin will be directed to the Admin View when selected from the nav bar. The view will contain a table with metrics and user information including username, first name, last name, email address, phone number, datetime of last login and lifetime visits. The user data will be stored in the PostgreSQL database. The user information will be collected at the time of registration thereafter datetime and lifetime visits will be updated with each login.


Figure 6 - Admin View
Table

































Project Milestones
If approval of this Scope of Work is received by The Company no later than March 24, 2016, at 2:30pm, development shall become effective on March 25, 2016, and the following deadlines will become effective. Changes, if necessary, will be reported by The Company via email to Nate.labatt@lakesmn.com The Client acknowledged and agrees that The Client's failure to adhere to deadlines will impact The Company's deadlines and estimated cost and, in such instances, The Company will not be responsible for missed deadlines, including final delivery/deployment, and increased costs and expenses.


Milestone
Responsibility
Date
Scope of Work Approved
Labatt Realty
03/24/2016
Server and Database
Company
03/25/2016
User View - Pages Wireframed, Zip Code Search
Company
03/29/2016
User View - Calculators, Results
Company
03/30/2016
Login View - Login, Password Change, File Hosting with Amazon Web Services
Company
04/01/2016
Admin View - Resources View, Upload CSV file, Styling, QA Testing, Styling
Company
04/06/2016

Schedule/Meetings

Event
Date
Time
Approval of Scope of work
Thurs, 3/24
1:30pm
Week 1 check-in
Fri, 4/1


Week 2 check-in
Fri, 4/9


Project Presentations
Wed, 4/13
12:00pm
Project turnover, end of contract
Fri, 4/15


Browsers
Application will fully support only the below listed browsers and QA will test only in the following browsers and versions. All browsers or versions not listed below are considered out of scope.

Browser Name
Version
 Google Chrome
49.0.2623.87

Devices
The devices that would be compatible to view the application will be Desktop, Mobile, and Tablet. The priority as dictated by order of importance from The Client will be Desktop, Mobile, and Tablet. Bootstrap will be used to ensure Mobile and Tablet compatibility.
Database
The primary function of the PostgreSQL database will be to store user information, including username, password (encrypted via hash), first name, last name, and phone number. The database will also be used to store analytics information, including the date of the user’s most recent login and the total number of times the user has logged in to the application. 
Information about house listings will not be stored in the database. Instead it will be pulled from a 3rd party API and sent directly to the user.
Technology
The Labatt Realty application will be built using the javascript-based MEAN stack (MongoDB, Express, Angular and Node). The front end user interface of the application will be built on the Bootstrap framework and use Bootstrap UI elements. Real estate data will be obtained from the SimplyRETS API. The application will bring in Google Analytics to track user behavior, and be viewable from the admin view of the application. Admin and client login will be handled with Passport user authentication. Google login is not conducive to monetizing the platform at a later date.   

Technologies and Versions Used:
JavaScript
HTML5
CSS3
Node.js 5.5.0
PostgreSQL 9.5.1
AngularJS 1.5.2
Angular-routes 1.5.2
Angular-animate 1.5.2
Angular-ui-bootstrap 1.2.5
Body Parser 1.15.0
Bootstrap 3.3.6
Express 4.13.4
Express Session 1.13.0
SASS 3.4.2
Passport 0.3.2
Pg 4.5.1
Stretch Goals
Favorites Feature - Allow registered users to store favorite house listings in a Favorites View
Social Media Links - Include social media links supplied by The Client
Image Carousel - Include an image carousel of available images in the Result Tile on the Home View
Support for more browsers 
Assumptions
While completing this estimate the following assumptions were made.
All changes to the Scope of Work after approval will require a re-evaluation of the Scope of Work.
All fonts, images, and stock photography will be provided by or billed to The Client. 
Clients and users of the application are using an appropriate, up-to-date web browser (see Browsers section). 
All costs of APIs, MLS access, file hosting, and server hosting are the responsibility of The Client.
Any other financial costs are the responsibility of The Client.
The Company assumes no responsibility for the success, failure or profitability of the workflows, methods, or business strategies created by The Client.
The Company is responsible for hosting and deploying the final version of this application.
Interactions with third party APIs assume that the API will not change during development and that the Terms of Service for the API allow the intended interaction.
The development timeline assumes all APIs are available and working during the development period. If APIs are unavailable, the project timeline will be affected.
Source Code
All source code produced by The Company for this project will be provided to The Client. The Client is free to work with other service providers on future modifications to the project utilizing the provided source code unless otherwise stipulated. The Company will retain a guest login account.

Approvals
By signing this document, I agree to the project outlined in this scope of work. If approval of this Scope of Work is received by The Company no later than March 24, 2016 at 5:00 pm, development shall begin by March 25, 2016.

Client Name (Print) ________________________________________________________________________  

Client Signature ___________________________________________________________________________




Client Name (Print) ________________________________________________________________________  

Client Signature ___________________________________________________________________________






























Amendment 03/25/2016


Above is a wireframe of the Home View with a search result that has been updated to reflect the use of the Zillow API. The Zillow API will replace the SimplyRETS API outlined in the first scope of work. With use of this API there will be changes in functionality of the web application. The users will be required to enter an address, city, state, and zip code in the search function on the Home View as opposed to simply a zip code with SimplyRETS. The API will return one result per search: the house at the address the user searched, with details populating a results field that will be a full-frame display. Information displayed will include an image carousel, address, Zestimate (Zillow’s home value estimate), square foot, price per square foot (using the Zestimate), use code, year built, bedrooms, bathrooms, and a link to get more information that links to Zillow. The branding requirements for the Zillow API require the ‘Zestimate’ valuation, the inclusion of a Zillow logo that links to Zillow and a link that reads ‘See more details for [address] on Zillow’. The user will click on one of two buttons, ‘Evaluate’ or ‘Mortgage’ to take them to the next page.






