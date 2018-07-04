



#**Verisi Co.**

Github Repo: https://github.com/samhager11/Verisi-Co.

Application Website: www.verisi.co

Trello Board: https://trello.com/b/yXU2VlDC


This application is built to fill the need for collaboration amongst individuals that want to join together in purchasing real estate properties as investment vehicles. This niche market is largely unrecognized by real estate professionals and instiutional investors alike. This, along with the fact that real estate data is very hard to access unless you are in the industry, means that there are very few tools that exist to serve the market of individuals investing in real estate.

The first implementation of this application was created to facilitate collaboration in the beginning stages of screening property acquisition targets.

A user who is logged in is able to add addresses of properties they have viewed on other websites. The application then makes API calls to Zillow for properties that the user decides to save to their profile. Collaboration is facilitated by the addition of groups that a user either creates or joins. A specific group name is attached to each saved property and allows the property to be viewed by members of the group. Think Google docs but with context that allows decisions to be made and actions to be taken quickly and efficiently.


##**Technologies**

This application was built using the MEAN Stack (MongoDB, Express, Angular, and Node). Node was used for the backend platform upon which the Express framework was implemented to facilitate routing. The application is connected to MongoDB and the database is hosted on MongoLabs.

Angular was used for the front-end application for its handling of routing for a single page application.

This app was built to have full CRUD functionality for its Users, Groups and saved Prospects(properties) within a RESTful structure. 

Additional UX Design was implemented via consultation during the creation of front-end functionality and design. 

##*Installation Instructions*

Additional npm packages were installed to aid the construction of the application and must therefore be installed using <npm install> in your terminal upon obtaining the source code.

##**Wireframes and Screenshots**

![Verisi Wireframe](./Readme-images/Schema_WireFrame.jpg)
![Verisi UX](./Readme-images/UX_Design.jpg)
![Verisi Home](./Readme-images/Verisi_home.png)
![Verisi Properties](./Readme-images/Verisi_map.png)
![Verisi Properties](./Readme-images/Verisi_tables.png)

##**User Stories**

User 1: I am a user who wants to get involved in real estate but doesn't know where to start. I need an app where I can save resources that I can quickly reference as I continue to learn more about investing in real estate.

User 2: I am a user who knows a number of individuals that want to go in on a real estate deal together but have no means of collaboration. I need an application that can save our potential investment targets for everyone in the group to view.
