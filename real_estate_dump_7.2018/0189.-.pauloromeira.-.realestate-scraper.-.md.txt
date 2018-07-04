# Real Estate - Scraper
A scraper that gathers data from real estate ads.

### Currently Supported Websites

|Country|Website|
|-|-|
|Brazil|[ZAP Imóveis](https://www.zapimoveis.com.br/)|

## Installation
|Requirements|
|-|
|[Python 3.6](https://www.python.org/)|
|[MongoDB](https://www.mongodb.com/) |

### 1. Clone this repository
Clone this repository using [git](https://git-scm.com/) and cd into the project folder:
```sh
git clone https://github.com/pauloromeira/realestate-scraper.git && \
cd realestate-scraper
```

### 2. Install Python requirements
Inside project folder, install python requirements using pip:
```sh
pip install -r requirements.txt
```

## Usage

First, run MongoDB server:
```sh
mongod &
```

Then use the following command to start crawling:

```sh
scrapy crawl zap [-a url=<zapimoveis-url>] [-a start=n] [-a count=n] [-a seed=<seed>]
```
> Curently, only [ZAP Imóveis](https://www.zapimoveis.com.br/) is supported  

**Arguments**:

* **count**: limits the number of pages the crawler will search for. The default is to crawl till the end.

* **start**: start crawling from a given page. The default is `1`.

* **url**: website url to perform search.

* **seed**: seed for the website search engine.

### Examples

* Default values - properties in Pernambuco, Brazil. Crawl all pages.
  ```
  scrapy crawl zap
  ```

* Olinda-PE. Crawl the first 4 pages.
  ```
  scrapy crawl zap -a count=4 -a urls="https://www.zapimoveis.com.br/venda/imoveis/pe+olinda/"
  ```

* Rio de Janeiro-RJ - south zone. Starting at page 100, crawl till the end:
  ```
  scrapy crawl zap -a start=100 -a urls="https://www.zapimoveis.com.br/venda/imoveis/agr+rj+rio-de-janeiro+zona-sul/"
  ```

* All places. Starting from page 4, crawl 3 pages:
  ```
  scrapy crawl zap -a start=4 -a count=3 -a urls="https://www.zapimoveis.com.br/venda/imoveis/"
  ```
