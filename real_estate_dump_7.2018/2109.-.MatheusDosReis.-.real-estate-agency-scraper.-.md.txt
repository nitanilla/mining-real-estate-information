# real-estate-agency-scraper

Project built to crawl Real Estate Agency websites. It can get the price, location and anything else.

Built using the tool [Scrapy](https://scrapy.org/), a [Python](https://python.org) framework to
extract data from web pages.

This project actually have spiders for the following websites:

| Country | Agency |
|-|-|
| Brazil | [Stória Imóveis](https://www.storiaimoveis.com.br/) |
| Brazil | [ImovelWeb](http://www.imovelweb.com.br/)|
| Brazil | [ZapImóveis](http://zapimoveis.com.br/) |
| Brazil | [VivaReal](https://www.vivareal.com.br/) |

## Dependencies

### Major

|Package|Version|
| - | - |
| [Python](https://python.org) | v3.6.5 |

### Python

| Package | Version |
| - | - |
| [Selenium](http://selenium-python.readthedocs.io/) | v3.12.0 |

### Extra

|Package|Version|
|-|-|
| [GeckoDriver](https://github.com/mozilla/geckodriver/releases)¹| v0.20.1 |

**¹ :** Geckodriver also can be installed using the command `npm install -g geckodriver`

## How to

### Clone the repository

To clone the repository, run in the command line:

```bash
git clone http://github.com.br/MatheusDosReis/real-estate-agency-scraper

cd real-state-agency-scraper
```

### Install python dependencies

Run the command bellow:

`pip install -r requirements.txt`

## Usage

### Spiders available

List of names of the available spiders:

* storia
* imovelweb
* zapimoveis
* vivareal

#### Run a spider

To crawl a specific spider:

```bash
scrapy crawl <name_of_the_spider>
```