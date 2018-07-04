realEscrape
======

My own real estate property listing


Real estate websites generally don't display PPSQM (Price Per SQuare Meter).

This small project scrapes property sizes and prices, and outputs a CSV with the PPSQM field added.
A blacklist can optionally be supplied, to filter out ads with descriptions that contain undesired terms.


#Dependencies
```
pip install scrapy unicodecsv unidecode
```

# Usage
```
# 1. Scrape "lebonoin.fr"
$ scrapy crawl leboncoin -o lbc.json
(...)
# 2. Filter the output against a custom blacklist
$ python analyze.py -b blacklist.txt lbc.json filtered.csv
Total/selected/censored: 641/323/318
# 3. Open `filtered.csv` in OpenOffice, and sort by PPSQM
```

