# Sahibinden.com Vehicle Data Fetcher [![GitHub stars](https://img.shields.io/github/stars/badges/shields.svg?style=social&label=Stars)](https://github.com/sirdavalos/Sahibinden-Vehicle-Data-Fetcher/)

[![Travis](https://img.shields.io/travis/rust-lang/rust.svg)](https://github.com/sirdavalos/Sahibinden-Vehicle-Data-Fetcher)
[![Repo](https://img.shields.io/badge/source-GitHub-303030.svg?maxAge=3600&style=flat-square)](https://github.com/sirdavalos/Sahibinden-Vehicle-Data-Fetcher)
[![Requires.io](https://img.shields.io/requires/github/celery/celery.svg)](https://requires.io/github/sirdavalos/Sahibinden-Vehicle-Data-Fetcher/requirements/?branch=master)
[![Scrutinizer](https://img.shields.io/scrutinizer/g/filp/whoops.svg)](https://github.com/sirdavalos/Sahibinden-Vehicle-Data-Fetcher)
[![DUB](https://img.shields.io/dub/l/vibe-d.svg)](https://choosealicense.com/licenses/mit/)
[![Donate with Bitcoin](https://img.shields.io/badge/Donate-BTC-orange.svg)](https://blockchain.info/address/17dXgYr48j31myKiAhnM5cQx78XBNyeBWM)
[![Donate with Ethereum](https://img.shields.io/badge/Donate-ETH-blue.svg)](https://etherscan.io/address/91dd20538de3b48493dfda212217036257ae5150)

Python script that grabs the data of the advertised vehicle from sahibinden.com and writes it to ***'inc/vehicle_data.csv'*** file.

***id_url.csv*** file contains the id of the advertisement and the url of it.

***vehicle_data.csv*** file contains the data of the real estate. 

### USAGE:
------
`python fetcher.py`

**NOTE:** There is a little bug in the script, sometimes fetcher.py ads the duplicate of the same row.I have created clear_csv.py script to delete the duplicates from .csv file.

### Instructions
------

0. Fork, clone or download this repository

    `git clone https://github.com/sirdavalos/Sahibinden-Vehicle-Data-Fetcher.git`

1. Navigate to the directory

    `cd Sahibinden-Vehicle-Data-Fetcher`

2. Install the dependencies

    `pip install -r requirements.txt`

3. Run the script

    `python fetcher.py`

4. Run clear_csv.py to clear the .csv file from duplicate entries

    `python clear_csv.py`

### CSV Attiribute Information
------

    1. TITLE      title of the ad
    2. ID         identification number of the ad
    3. PRICE      price of the vehicle
    4. CURRENCY   currency of the price    
    5. LOCCITY    city of the ad
    6. LOCOUNTY   county of the ad
    7. LOCDIST    distirct of the ad
    8. LAT        latitude of the location of the ad
    9. LON        longitude of the location of the ad
    10. DATE      ad release date
    11. BRAND     type of the ad
    12. SERIES    series
    13. MODEL     model
    14. FUEL      fuel type
    15. YEAR      manifactured year
    16. GEAR      gear type
    17. KM        total kilometers driven
    18. FRAME     body frame
    19. ENGVOL    engine volume
    20. HP        horse power
    21. DRIVE     front or rear drive
    22. COLOR     color
    23. WARRANTY  warranty
    24. PLATE     saler of the flat is owner, real estate office or construction company
    25. SALER     saler of the flat is owner, real estate office or construction company
    26. STATUS    saler of the flat is owner, real estate office or construction company
    27. EXC       exchange is possible or not

6. Missing Attribute Values:  None.

### LICENSE
------

MIT License