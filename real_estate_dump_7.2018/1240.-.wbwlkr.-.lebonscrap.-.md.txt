# LeBonScrap

## Description

LeBonScrap is a spider which collect data from [Leboncoin.fr](https://www.leboncoin.fr), a french portal for selling new and second hand goods throughout the whole country.

The spider will crawl all the pagination links to scrap every ads of the list from one search result of the real-estate category.

To extract the data, LeBonScrap uses the open source and collaborative framework [Scrapy](https://github.com/scrapy/scrapy).

## Installation

To download the script, type the code below in a shell :

```shell
git clone git@github.com:wbwlkr/lebonscrap.git
```

## Getting started


Run the lebonscrap.py spider using the runspider command:

```shell
scrapy runspider lebonscrap.py -o data.json
```

For each ads,the data related to the following columns will be written in a json file or csv:

```
'Url':
'Titre'
'Prix'
'Surface'
'GES'
'Classe énergie'
'Auteur'
'Téléphone'
'Remarques'
```

## Requirements

 * Python3
 * Scrapy==1.4.0

## Author

* **[WebWalker](https://github.com/wbwlkr)**

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
