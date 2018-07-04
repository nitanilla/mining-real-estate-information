# Capstone Senior Project
This group project was developed as our Senior Capstone Project during our last semester at Baylor University. This project was given to us by [Pariveda Solutions](http://www.parivedasolutions.com/Pages/default.aspx). The goal of this project was to integrate all of the knowledge learned throughout college and apply it in a situation that resembled situations found in industry. We were given a *fictional problem* and we had 15 weeks to implement a solution for such a problem (described below).

## Group Members
- [Andy Sapper](https://www.linkedin.com/in/andysapper)
- [Brennan Saul](https://www.linkedin.com/in/brennansaul)
- [Collin Rapp](https://www.linkedin.com/in/collinrapp)
- [Ryan Ragnell](https://www.linkedin.com/in/ryanragnell)

### Business Problem
"Commercially Facilites Management"

Commercially is a leading (fictional) commercial real estate services and investment firm. The core of their business revolves around leasing, servicing and maintaining commercial properties used for office space, retail, medical centers, malls, hotels, warehouses etc. Commercially prides itself on being able to meet its client's most demanding real estate challenges by leveraging their diverse set of global listings.

Commercially manages buildings with many tenants all over the world. A strenuous task with managing commercial properties is the management of supplies, i.e., paper towels, toilet paper, etc. When tenants run out of certain supplies, the process of scheduling someone to go replace said supply is time consuming. Commercially wants to automate this scheduling and provide maintenance employees with schedules to replace supplies.

## Our Solution
Our solution consists of a web application and a cross-platform mobile application that handles maintenance requests and schedules them to the maintenance workers.

### Technology Stack
For this project we used a MEAN stack, which is comprised of the following technologies:

- MongoDB
- ExpressJS
- Angular (with use of Ionic for mobile application)
- NodeJS

We used MongoDB as our database engine, ExpressJS as our API framework, Angular as our front-end framework, and NodeJS as the framework to build the application on. For our mobile application, we use the Ionic framework.

For our server we chose to use [**CentOS**](https://www.centos.org/), which is an open source software that suited our needs. We chose it because it is robust enough and also because it is widely trusted by the community of developers.

Inside our server we run our application with [**Docker**](https://www.docker.com/). With Docker we are able to abstract some configuration away from the server itself and handle it inside the Docker containers. This allowed us to freely make and test configuration changes without having to worry about causing costly configuration breakdowns. 

#### Reasoning For Technology Stack
We decided to use the MEAN stack for several reasons:

1. The MEAN stack is widely used and receives a lot of support from the community of developers.
2. The MEAN stack uses one language, Javascript, across all frameworks. Thus, it makes development very smooth and seamless among the frameworks.
3. MongoDB provided us with a lot of flexibility in terms of our database structure. This aspect was particularly relevant since we knew our database structure would most likely change often as we made changes to our product.
4. ExpressJS provided us with an API that required little setup and was very robust.
5. Angular provided us much flexibility on our front-end.

### Priorities
Our product focused primarily on three different aspects:

- Security and robustness
- Simple and intuitive interfaces
- Versatility

We wanted our product to be very robust in handling all of the internal and external operations: communications and operations between all of the components. We also wanted it to be simple to use: anyone should be able to use our product without needing to read a user manual. Lastly, we wanted it to provide the users a whole range of options with regards to how they handle the requests made.


## Design Overview
Following is an overview of our product, which is comprised of five different actors:

- FLIC buttons (bluetooth low-energy): single click (only event used in this product), double-click, and hold click.
- Raspberry Pi: listens for button events and communicates them to the server.
- Server: handles communication from Raspberry Pi, Mobile and web applications.
- Mobile application: provides a mobile interface for the users.
- Web application: provides a desktop web interface for the users.

![Design overview diagram](https://s13.postimg.org/y9ztxcgqv/Design_overview.png "Design overview diagram")

### Detail
The FLIC button, once clicked, communicates with the Raspberry Pi, which in turn listens to button events and communicates them to the server through a known API. The server stores these button events and handles them appropriately. The mobile and web applications communicate with the server to perform different operations.


## File Structure
Our file structure is divided into separate modules, which translate to containers inside Docker. The project is divided into the main categories, which are:

- Markdown: folder including this documentation :)
- database: folder including all the files used to configure MongoDB.
- pushstock-app: folder containing the source code for our server and front-end components.
- raspberry-pi: folder including the source code for our button controller.

## Layer Architecture Design
We chose to use a modular design so that each component could depend as little as possible on other major components. Thus, the coupling between components (i.e., the Raspberry Pi and the server) was kept at a minimum, while each component was given a substantial set of responsibilities. Our architectural design is as follows:

![Layer architecture diagram](https://s18.postimg.org/f39jcdzbd/Layer_architecture.png "Layer architecture diagram")

The API in our server is the only actor allowed to make changes to the database; this allows us to control all interactions with the database. The API is the only communication point between the server and the mobile/web applications and the Raspberry Pi. The mobile/web applications' communication with the API is handled through the use of services, which provide us with reusable pieces of code. Beyond that, the mobile/web applications are divided into components, which further embrace the modular design we adopted. The Raspberry Pi directly communicates with the API to communicate the event of a single button click.

## Detailed Design
Following is the detailed design for the layer presented above.

### Database
Our database consists of three main schemas:

- Button: represents the FLIC button used by workers
- Employee: represents the Administrator and Maintenance workers
- Task: represents the requests being made by button events

![Database diagram](https://s1.postimg.org/m1mkofzrj/Database_diagram.png "Database diagram")
