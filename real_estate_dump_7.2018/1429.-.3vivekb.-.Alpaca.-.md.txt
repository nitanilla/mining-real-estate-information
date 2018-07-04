# Alpaca: An Economic Evaluation Plug-In for Scenario Planning Tools
The "Alpaca" project, funded by the Lincoln Institute of Land Policy (http://www.lincolninst.edu/), developed software designed to facilitate the integration of bid-rent land use models with scenario planning tools.  Such models can enhance scenario planning efforts by simulating how real estate markets work, adding a variety of metrics relating to topics such as:
* Property value and rent
* Socio-economic characteristics of tenants
* Housing affordability and cost burden

This repository provides a homepage for the code developed in the course of the project, including:
* mu-land: the "core" bid-rent model evaluation software
* muLandWeb: a Python wrapper for mu-land allowing models to be offered as web services callable by third-party tools
* example: client-side Python scripts developed in case studies, showcasing various methods of using mu-land

# Requirements
The server-side software (mu-land and muLandWeb) has been tested using Linux, specifically Ubuntu 14.04 LTS.  Other distributions and/or operating systems may work, but there are no guarantees.  Some of the client-side scripts demonstrate how models could be called from other environments.

The mu-land core uses Boost 1.54 libraries.

PostgreSQL is used for back-end database management and spatial operations involving PostGIS.

A bid-rent land use model is required in order to apply the framework.  Regional planning agencies using the Cube Land software distributed by Citilabs (see http://www.citilabs.com/) may have existing models in a format very similar to that required by mu-land.  Manhan Group, LLC (http://manhangroup.com/) has developed many of these models and provides related consulting services.

# Installation steps
The mu-land program must be installed first.  Follow the instructions in the "readme" file within the mu-land folder.

Then, do the following:
 1. Edit /etc/apt/sources.list, adding ```deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main```
 2. Install required packages:
 
  ```Shell
  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
  apt-get update
  apt-get dist-upgrade
  apt-get install python3 python3-dev python3-pip python-virtualenv postgresql-9.5 postgresql-9.5-postgis libpq-dev
  ```
 3. Configure PostGIS as needed.
 4. Install muLandWeb:
 
 ```Shell
 mkdir mulandweb
 cd mulandweb/
 virtualenv -p `which python3` env
 . env/bin/activate
 pip install https://github.com/ManhanGroup/Alpaca/archive/master.zip
 ```
 5. Create mulandweb/bin directory and copy mu-land into it as muland
 6. Initialize tables at the database using ```python -m mulandweb -c```
 7. Unpackage model into mulandweb directory and import e.g. ```python -m mulandweb -i fresno --import-srid 900913```
 
# Credits
* Software design/testing: 
 * Colby Brown (colby@manhangroup.com)
 * Pedro Donoso (pedrodonosos@gmail.com)
* Programming:
 * Felipe Saavedra (fsaavedr@dcc.uchile.cl)
 * Leandro Lima (leandro.lima@toptal.com)
