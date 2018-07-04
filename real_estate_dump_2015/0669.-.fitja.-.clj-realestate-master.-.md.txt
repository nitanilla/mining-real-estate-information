# Realestate

Small Clojure web application for real estate ads.
This project uses libraries: [Compojure](https://github.com/weavejester/compojure), [Ring](https://github.com/ring-clojure/ring), [Hiccup](https://github.com/weavejester/hiccup), [CongoMongo](https://github.com/aboekhoff/congomongo), [Mongo-session](https://github.com/amalloy/mongo-session), [Lib-noir](https://github.com/noir-clojure/lib-noir) and [Clj-time](https://github.com/clj-time/clj-time). 
Some available options in this project are: discover real estate ads, register new user account, login. Logged in users are allowed to maintain ads (insert new, update or delete existing). 
There are some preinserted reale state ads, and one default user "admin", pass: "adminadmin". 
Before entering new data into DB, application performs some basic validation checks.

## Usage

Download and install [Leiningen](https://github.com/technomancy/leiningen)

Download and install [MongoDB](http://www.mongodb.org/downloads)

Start MongoDB.

Start application from command line - cd to project location - lein run. Default browser will open web page.

##References

Clojure programming, Chas Emerick, Brian Carper and Cristophe Grand

Developing and Deploying a Simple Clojure Web Application and A brief overview of the Clojure web stack for learning Ring, Compojure and Hiccup

CongoMongo library for using MongoDB with Clojure - mongo.clj

Hickory library for parsing HTML used to extract data from web page - extract_data.clj.

## License

Distributed under the Eclipse Public License, the same as Clojure.
