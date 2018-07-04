# Mobclip

Mobclip is a pet project that crawls real estate data from a website.
The motivation behind is that I would like to have a better view on prices and
do some analysis based on neighbourhood and price per square meter. In addition, 
I would like to monitor prices in order to discovery raises and discounts.

This project uses the following technologies:

* jsoup - world class HTML parser
* Spring Boot - my new best friend
* Apache Kafka - publish and subscribe to streams of data
* MongoDB - document database designed for ease of development and scaling
* Spring Data MongoDB - persistence layer
* commons-cli - provides an API for parsing command line options passed to programs

### How it works

The first step is to get the number of pages returned by the website according to your
search criteria (Ex: houses or apartments, sell or rent, etc). It is easily done
by jsoup. Each page lists about 24 records.

For each page we produce a message (it is simply a URL with query parameters) for Kafka.
So, if you have 200 pages you have 200 messages. 

The second step consists in consuming those messages. For each message we extract some
basic information about the property such as price, address and its URL for detailed view
and create a Property object. For each Property, we produce a message for other Kafka topic.

The third step is responsible for extracting detailed information (total area, building area, etc) 
about the property. Once all necessary data is extracted more messages are produced for the last Kafka topic. 

The last step consumes Property objects and persists them on MongoDB.

### Current status

At this time there is no front end. Analysis is made by querying documents on MongoDB.

Price monitor is not hooked in the processing yet.

### How to run

Check the Kafka topics at Topics.java

Check Consumer factory at ConsumerFactory.java for configuration

Check Producer factory at ProducerFactory.java for configuration

To run the application check Application.java. It is possible to configure the application mode
and run different parts of processing on distributed JVM's. You can also configure the number
of threads for each step. If you want to run it on a single machine and JVM use standalone mode.

### NOTICE

It is for personal use only.




