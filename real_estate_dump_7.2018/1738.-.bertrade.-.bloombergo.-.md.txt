# bloombergo

Scrapes Bloomberg and generates a JSON file with general information based on a list of tickers or text file.

The
heavy lifting is done by BeautifulSoup and the amazing [PyWebRunner](https://github.com/IntuitiveWebSolutions/PyWebRunner) so it requires a browser. For now it uses Chrome so you need that webdriver for Selenium. Firefox can be easily added, I simply don't use it.


### Usage

```
bloomberg.py [-h] [-f FILE] [-t tickers [tickers ...]]
                    [--export-skipped]

Scrapes Bloomberg for multiple tickers and generates a .json file at /tmp
based on a list of tickers.

optional arguments:
  -h, --help            show this help message and exit
  -f FILE, --file FILE  Input text file for tickers (one per line)
  -t tickers [tickers ...], --tickers tickers [tickers ...]
                        Tickers list (eg. "ALSEA*:MM", "AC*:MM")
  --export-skipped      Exports skipped tickers to a text file at /tmp
```

### Quick setup for mac:

```
brew install chromedriver
virtualenv venv
./venv/bin/pip install -r requirements.txt
./venv/bin/python bloomberg.py
```

### Examples for Mexican Stock Exchange (BMV)

Get tickers from CLI arguments:

`./venv/bin/python bloomberg.py "ALSEA*:MM" "AC*:MM"`

Get tickers from text file:

`./venv/bin/python bloomberg.py -f stock_list_bmv.txt`

Will generate a JSON file under `/tmp` like this one:

```javascript
[
  {
    "sector": "Financials",
    "profile": "Corporacion Inmobiliaria Vesta SAB de CV is a real estate owner, developer and asset administrator of industrial buildings and distribution centers in Mexico. The Company is focused in the development of world class facilities for specific industries such as aerospace, automotive, logistics, food and beverage, medical devices and electronics, among others.",
    "name": "Corp Inmobiliaria Vesta SAB de CV",
    "industry": "Real Estate",
    "sub_industry": "Real Estate Owners & Developers",
    "ticker": "VESTA*:MM",
    "market": "Mexico",
    "board_members": [
      "Lorenzo Manuel Berho Corona",
      "Juan Felipe Sottil Achutegui",
      "Lorenzo Dominique Berho Carranza",
      "Alejandro Ituarte Egea",
      "Alejandro Pucheu Romero"
    ]
  }
]
```
