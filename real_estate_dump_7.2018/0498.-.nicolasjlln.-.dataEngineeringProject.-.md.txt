# Data Engineering Project

The Data Engineering project is a school project done during the 4th year of engineering school at ESIEE Paris.</br>
The aim of this project is to scrap and store data from a website. Then, the goal is to permit the data access trough a local web portal. In this project, we had to scrap, store and make accecible data from a real estate website, called [ORPI](https://www.orpi.com/?utm_source=bing&utm_medium=cpc&msclkid=26b36418dde91e469c873efcb7e2f34b&gclid=CMnUhJn93NoCFUbNGQodJqcEVA&gclsrc=ds "ORPI website").

## Getting Started

The project is runnable via a docker container.</br>
That's all.

The instructions below are destined to a Linux based usage. This doesn't mean the project won't work on another environment, but the instructions to do so aren't displayed here.

### Prerequisites

* This library is __built with Python 3__.

> If you do not have Python 3 on your computer, to install it with linux is :
```
$ sudo apt-get update
$ sudo apt-get install python3.6
```
(or follow this [link](http://docs.python-guide.org/en/latest/starting/install3/linux/ "Python 3 installation"))

* Make sure you have __docker__ on your computer.

> To install Docker with pip (Python 3) :
```
$ pip3 install docker
```

### Installing

* You must clone the git dir or download it on your computer.
```
$ git clone https://gitlab.com/nicolasjlln/dataEngineeringProject
```

* Using Docker, you have to build the Docker images and run them. Open a terminal and enter the commands in that order):
```
$ docker run -d --name mongo -p 27018:27017 mongo
$ docker build -t scrapy -f Dockerfile_scrapy .
$ docker build -t flask -f Dockerfile_flask .
$ docker run -d --name flask --link mongo -p 5000:5000 flask
$ docker run -it --name scrapy --link mongo scrapy
```
*If you need a Docker tutorial and/or explore its possibilities, go to [this link](https://docker-curriculum.com/ "Docker tutorial")*

* Once you are in the docker image with the '**docker run**' commands, the required libraries should have been installed and our application is ready to be used !

## How it works

### Basic application

Our project lies in building the web application, coded with the Python framework __Flask__.
The scrapped and stored data are information about property advertisements in the ORPI web site.

Basically, the web app is used only for displaying the information. But it contains an __advance search function__, to order the results and/or get more relevent information.

To access the web portal, you will have to open a browser, and go to this [link](http://localhost:5000 "Web portal") :
```
http://localhost:5000
```
Then, you are in the app, enjoy !

### To go further

The application is designed to scrap only 12 agencies, for efficiency reasons. Note that if you run the app every hour, the results won't be the sames since the OPRI website changes its announces quite often.

__But this number of scrapped announces can be changed !__
For this, you will have to modify one file :
```
. Project
|__ orpi
      |__ spiders
               |__ opri_spider.py  <- In this one !
```

Open it with a text modifier, go in the `OrpiSpider` python class, and in the `parse(...)` function, until you find this line :
```
agencies = agencies[0:<max_number>]
```
Initially, `<max_number>` is set to 12. But it can take any value !

Once you modified it, save it, close it and run the app again (go back to the app root directory first).

## Built With

* [Flask](flask.pocoo.org/) - Permited to build the web application
* [MongoDB](https://www.mongodb.com/fr/) - Used for data managment
* [Scrappy](https://scrapy.org/) - Brilliant scrapping framework

## Authors

* **Nicolas JULLIEN** - [nicouilla](https://gitlab.com/nicouilla)
* **Vincent DECKER** - [VincentDecker](https://gitlab.com/VincentDecker)
* **Yoann GALLOCHAT** - [yoannEsiee](https://github.com/yoannEsiee)
* **Alexandre NORET** - [alexandre-noret](https://github.com/alexandre-noret)

See also the list of [contributors](https://github.com/nicolasjlln/dataEngineeringProject/settings/collaboration) who participated in this project.

## License

This project is licensed under the ESIEE Paris License.

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
