# Listing Database

This project contains all files necessary to the creation of the web app: "real estate app". This app perfrms CRUD operations for a database storing data about the listing of a real estate agency.

### Table of Contents

* Install
* What's Included
* Running the app

### Install

> Listings Database requires Python 2.7 or higher and SQLAlchemy to be installed on your computer in order to be executed.
> Please make sure that Python 2.7 or higher is installed on your computer or download and install it.
* [Windows](https://www.python.org/ftp/python/2.7/python-2.7.amd64.msi)
* [Mac](https://www.python.org/ftp/python/2.7/python-2.7-macosx10.5.dmg)

> Linux user should have a version of Python already installed. Please refer to appropriate distribution documentation
> and upgrade to a newer version if needed.

> Please make sure that SQLAlchemy is installed on your computer or download and install it following the instructions at:
* [SQLAlchemy](http://www.sqlalchemy.org/download.html)

### What's Included
```sh
catalog/
|--application.py
|--client_secret.json
|--database_setup.py
|--fb_client_secrets.json
|--README.md
|--saved_listings.py
|
|--static/
|  |--styles.css
|  |--top-banner.jpg
|
|--templates/
   |--deleteListing.html
   |--deleteRoom.html
   |--editListing.html
   |--editRoom.html
   |--header.html
   |--listings.html
   |--login.html
   |--main.html
   |--newListing.html
   |--newRoom.html
   |--publiclistings.html
   |--publicroom.html
   |--room.html
```

### Getting Started with Udacity UD-197 course material



The following instructions are supposed to work out of the box on Vagrant VM:
* Install Vagrant VM as descibed [here](https://www.udacity.com/wiki/ud197/install-vagrant)
* Download the catalog project from [GitHub](https://github.com/marscar)
* extract it on your local machine. **Keep all files in the same folder!**
* Open a terminal (Mac, Linux) or Putty (Windows)
* Crawl to the VM folder
```sh
$ cd /home/../path_to_VM_folder/fullstack/vagrant
```
type 
```sh
$ vagrant up
$ vagrant ssh
```
to launch your virtual machine andd log into it;

* Crawl to the project folder
```sh
$ cd /vagrant/catalog
```

First lets create the database including three tables: Listing, Room and User

1) type
```sh
$ python database_setup.py
```

This step is optional! Included in /catalog is the file saved_listings.py; this file include instances of the Listing, Room and User classes. You can run saved_listings.py if you want to start populating the tables of listings.db, previously created. If you want to achieve full control over the preloaded data, substitute the credentials of the dummy user with your own and start exploring the capabilities of "real estate app".

2) type
```sh
$ python saved_listings.py
```

Register the app. "real estate app" implements OAuth2 security protocols, implemented through third party providers: Google and Facebook. 

3) Register your app and request App ID and App Secret at [Google](https://console.developers.google.com/project) and [Facebook](https://developers.facebook.com/)

4) Replace client_secrets.json with the json file provided by Google; substitute the values in the file fb_client_secrets.json with the ones provided by Facebook

5) Open login.html in your favorite editor and:
* replace the value of data-clientid with the one you obtained from Google
* replace the value of data-appId with the one you obtained from Facebook

Build "real estate app"

6) type
```sh
$ python application.py
```

7) Start your favorite web browser and go to http://localhost:8000

### Author
Marcello Scarnecchia

