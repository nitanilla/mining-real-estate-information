# Byt Objevitel ("Flat/Apartment Explorer")

This project aims to be a continue development and learning experience for those attending the [Learn by doing](http://www.meetup.com/Life-Learning-Programming-Prague/) meetup group. Each week we will focus on one area of the project so that we can learn in-depth about each individual part of a web application.

Besides developing your skills and helping you learn through real experience, we would like to build something that is actually useful for end-users. To achieve this, we must first know what we want to build:

> Byt Objevitel will provide a web site and/or app that will make finding a flat (in the Czech Republic) easier. It will do this by combining the real-estate data from multiple different sources and by providing some additional tools to search for and find a flat.


## High-level Technical Specification

* __Gather data__ about the real-estate market in the Czech Republic from various sources. For example:
  * reality.idnes.cz
  * www.bezrealitky.cz
  * www.sreality.cz
* __Store raw data__ in a database to be processed and analyzed later.
* Create a __web interface__ to search and display the data. This is what our end-users will see. They will use the web site to specify exactly what kind of flat they are looking for.

For specific things that are still left to do, have a look at the [issue tracker](https://github.com/Learn-by-doing/byt-objevitel/issues) for this project.


## Requirements

To work on this project, you will need the following:
* Your own [GitHub](https://github.com/) account
* [Git](https://git-scm.com/downloads) - A program for managing a project's change-log / history
* [Node.js](https://nodejs.org/) - A platform for running JavaScript programs.
* [MySQL](https://dev.mysql.com/downloads/mysql/) - A database server that allows storing, analyzing, and retrieving data.


## Getting Started

Before you continue, be sure that you have all the necessary [Project requirements](#requirements) for this project.

### Create Your Own "Fork" of this Project

"Forking" is like creating a copy of a project. While logged in to your GitHub account, ["fork" this repository](https://github.com/Learn-by-doing/byt-objevitel/fork). This will create a copy of the project, but in your account.

Once you've created your fork, you will need to download a copy of the git repository to your local machine. To do this you will "clone" the repository using the following command in the terminal window where you use git:
```
git clone https://github.com/YOUR_USERNAME/byt-objevitel.git
```
Be sure you replace **YOUR_USERNAME** with your GitHub username.


### Installation

Like any [node.js](https://nodejs.org/)-based project, you will need to install any node modules that the project depends on. To do this you will use npm. Run the following ccommand from within the project directory:
```
npm install
```


