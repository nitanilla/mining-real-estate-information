# Real Estate Data Sources Notes

This repository is a place to track any possible data sources explored by contributors to the project.
If you are interested in contributing a source, please follow these steps:

1. Find a good data source
1. Check if any previous contributor has researched your source.  If no, please start.  If yes, check if their approach should be updated in any way.
1. Do a complete investigation (no random links without research, please) following the steps in the next session
1. Clone/fork this repo
1. If no file exists for the country you're working on, please follow the pattern and create a file.
1. Modify the [country]/datasources.json file with your changes.
1. Send a pull request with your changes/additions.
1. Wait for confirmation
1. Pat yourself on the back!

## Picking a place to research

The project is looking for data sources that provide substanative programatic access to historical and recent/current real estate sales data.
Other contributors to the Data Skeptic Home Sales Data Project may come here to find good sources, and write crawlers/parsers/agents that will
retrieve data on a schedule from these sources, and send it to the project API.  In this fashion, a distributed set of independent applications
can be built, managed, and maintained by those interested in particular data sources can provide a more robust ecosystem for centralizing / 
democratizing this data.

## Objectives

For finding sources, our objectives are:

* Find new sources of data
* Confirm the source is accurate
* Confirm programatic access is available
* Ensure that any consumption of the datasource for use by you or others involved in the project does not violate the datasource's terms of service
* Do an example use of the data pull from this source, upload it somewhere publically on the internet
* Update the json files in this repo and send us a pull request

## Schema

```json
{
    "name": "For Sale By Owner"
  , "main_url": "http://www.forsalebyowner.com"
  , "date_last_checked": "2016-03-20"
  , "checked_by_git_user": "kylepolich"
  , "has_current": "yes"
  , "has_historic": "no"
  , "states_covered": "all"
  , "example_api_url": "http://www.forsalebyowner.com/search/list/los-angeles-california/house,condo-types/0-page/proximity,desc-sort"
  , "example_use": "http://dataskeptic.com/blog/b009_Crawling-forsalebyowner.php"
  , "notes": [
    {"author": "kylepolich", "date": "2016-03-20", "note": "Disappointing, but good example of a quick parse"}
  ]
}
```
