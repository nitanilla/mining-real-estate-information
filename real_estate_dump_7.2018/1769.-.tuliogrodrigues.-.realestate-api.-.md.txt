# Real Estate API
This is a RESTfull API to represents a simple Property CRUD

## Technologies

 - **Spring-Boot** to create a stand-alone Spring based application
 - **Mongo** as database;
 - **Lombok** to generate constructors, getters, setters hashcode and equals methods
 - **Swagger** to get a nice API documentation
 - **Fongo** a fake mongo to use on tests

## Installation and Getting Started

You must have Docker and Docker Mongo Image, [here is a documentation to how to do it](https://hub.docker.com/_/mongo/)

**PS**: To start Docker Mongo Image, use de follow command:

> sudo docker run -ti --net=host mongo

After that you can run real estate application running with command

> gradle bootRun

and It's done, now you can access the project, or even better the swagger-ui by address :

> localhost:8080/realestate/swagger-ui.html
