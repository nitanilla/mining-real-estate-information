# Sahibinden.com Real Estate Data Fetcher [![GitHub stars](https://img.shields.io/github/stars/badges/shields.svg?style=social&label=Stars)](https://github.com/sirdavalos/Sahibinden-Realestate-Data-Fetcher/)

[![Travis](https://img.shields.io/travis/rust-lang/rust.svg)](https://github.com/sirdavalos/Sahibinden-Realestate-Data-Fetcher)
[![Repo](https://img.shields.io/badge/source-GitHub-303030.svg?maxAge=3600&style=flat-square)](https://github.com/sirdavalos/Sahibinden-Realestate-Data-Fetcher)
[![Requires.io](https://img.shields.io/requires/github/celery/celery.svg)](https://requires.io/github/sirdavalos/9GAG-Media-Downloader/requirements/?branch=master)
[![Scrutinizer](https://img.shields.io/scrutinizer/g/filp/whoops.svg)](https://github.com/sirdavalos/Sahibinden-Realestate-Data-Fetcher)
[![DUB](https://img.shields.io/dub/l/vibe-d.svg)](https://choosealicense.com/licenses/mit/)
[![Donate with Bitcoin](https://img.shields.io/badge/Donate-BTC-orange.svg)](https://blockchain.info/address/17dXgYr48j31myKiAhnM5cQx78XBNyeBWM)
[![Donate with Ethereum](https://img.shields.io/badge/Donate-ETH-blue.svg)](https://etherscan.io/address/91dd20538de3b48493dfda212217036257ae5150)

Python script that grabs the data of the advertised real estate from sahibinden.com and writes it to inc/real_estate_data.csv file.

id_url.csv file contains the id of the advertisement and the url of it.

real_estate.csv file contains the data of the real estate. 

### USAGE:
------
`python fetcher.py`

**NOTE:** There is a little bug in the script, sometimes fetcher.py ads the duplicate of the same row.I have created clear_csv.py script to delete the duplicates from .csv file.

### Instructions
------

0. Fork, clone or download this repository

    `git clone https://github.com/sirdavalos/Sahibinden-Realestate-Data-Fetcher.git`

1. Navigate to the directory

    `cd Sahibinden-Realestate-Data-Fetcher`

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
    3. PRICE      price of the flat
    4. CURRENCY   currency of the price    
    5. LOCCITY    city of the building
    6. LOCOUNTY   county of the building
    7. LOCDIST    distirct of the building
    8. LAT        latitude of the location of the building
    9. LON        longitude of the location of the building
    10. DATE      ad release date
    11. TYPE      type of the ad
    12. M2        size of the flat in meters
    13. ROOMS     Rooms in flat
    14. AGE       age of the building
    15. FLOOR     floor number of the flat
    16. TFLOOR    number of floors in building
    17. HEAT      heating type of the building
    18. BATH      number of bathrooms in the building
    19. FURN      flat is furnitured or not
    20. STATUS    occupied by owner, lessee or empty
    21. RESID     building is in residence or not
    22. DUE       monthly dues of the building
    23. LOAN      flat is available for loan or not
    24. SALER     saler of the flat is owner, real estate office or construction company
    25. EXC       exchange is possible or not

### LICENSE
------

MIT License