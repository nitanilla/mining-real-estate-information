# YYC Homes Scraper

A quick tool to help sift through real estate data.

_This was just an experiment, not a general-purpose tool._

## Setup

Data will be sent to ElasticSearch. This codebase expects ElasticSearch to be running on localhost at port 9200. Before your initial scrape, it is recommended to first create a template for your index by running `bash create_template.sh`.

### Install Dependencies

```sh
pip install -r requirements.txt
```

## Run

```sh
scrapy crawl calgary-real-estate.com
```
