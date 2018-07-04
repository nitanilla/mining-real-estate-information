# Partmint :herb:
	Developed By: Mihir Naik, Chase Morris and Chakrit Prasatwattana
## Table of Contents

- Purpose
- Used Technologies
- Unsolved Problems
- How To Use
- References


### Purpose
------
  This web application was designed to do a better job of connecting the Owners of different properties (apartment complexes and/or homes) to the tenants. Whether the connection being made is to notify about rent being due, maintenance requests or a complaint. Partmint has the API to do those very things, plus give guests to the site the opportunity to inquire about vacant properties. 
	Seeing a need for this application at a local real estate business, certain features for Property Owners were implemented. Logging in as a Property Owner gives you the ability to not only showcase your new properties but also manage current and potential residents. Overall, using Partmint gives people in the real estate business better control over managing their business.

***important information can go here.*** 

### User Stories and ERD Diagrams
---
The user stories and ERD diagrams can be found on the trello board at this [link](https://trello.com/b/YDgBtdo4/partmint)

### Used Technologies
---

Partmint makes use of key API's and Databases

HTML: To Display text on different pages of the site

CSS/Bootstrap: To style the text, navbar, modal,carousel ,links and forms found through out the site 

Javascript: Create the functionality between the users(property owner/resident) and server.

Jquery: to traverse the DOM 


Ajax: Used ajax to create chate between residents adn property owner

Node.js: allows us to runs javascript not in the browser. Implemented Node Module Packages: 

	 Express
	 Mongoose
	 Body-Parser
	 Morgan
	 EJS
	 Express-EJS-Layouts
	 Connect-Flash
	 Cookie-Parser
	 Express-Session
	 Underscore
	 Passport
	 Dotenv
	 Connect-MongoDB-Session
	 Sweetalert

MongoDb: A database to store information about the Property Owner, Resident and Property.

Stripe: a payment API so residents can make payments for their rent




### Unsolved Problems 
---
 Currently the team have not implemented complete security functions to Partmint. In 
	in addition there are still design elements that need to changed to create a better user expereince. 

### How to Use
---
Go to https://partmint.herokuapp.com to check out the site. Click on `All Properties` to browse through the different properties available for rent. Click on a specific property to Apply for that apartment. From the main page you can also  Log in to view your dashboard as a resident or owner. From the dashboard you can view information regarding rent, properties,group notices and indiviudal notices.

### References
---
 	- https://stripe.com/docs
 	- https://trello.com/b/YDgBtdo4/partmint
	- https://fonts.google.com/