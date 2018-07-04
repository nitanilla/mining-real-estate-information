# spoofDog
Web scraper designed to collect data about real estate projects (availability, price (WIP) , ...)

This tool is meant to regulary scrape web pages of real estate development projects and collect data about availability of flats (appartments) in projects and their prices, specificaly checking for market spoofing (pretending high demand and sold out flats).

Program has two main parts, scraper that does actual data collection and web interface (work in progress) that provides visualization of collected data.

## Collector
To collect data from all projects that are currently set as `active` in `config.yml`, run `collector/collector.py` script. This should be done regulary to yeild meaningfull results.

## Extensibility
Web scraper (in collector subdirectory) is designed to be modular for easy extensibility to include new real estate projects. To create module for new project, look for existing examples in `estate_modules` directory. There you need to to create new `.py` file that contains class inheriting from `RealEstate`.
Your new class must override `get_data` method that fills `self.data` dictionary with flat identificators (keys) and information about their availability (values). To preserve consistency between multiple projects, data in final dictionary should follow unified scheme when indicating availability. `RealEstate` class contains constans that help with this:

1. `RealEstate.free_const` - Marks free flat / appartment (default value: 'F')
2. `RealEstate.reserverd_const` - Marks reserved flat / appartment (default value: 'R')
3. `RealEstate.sold_const` - Marks sold flat / appartment (Default value: 'S')

After creation of new module, it must be added to config file (`config.yml`) as new key under `Projects`. This key must match modules filename and should contain following attributes:
 * `human_name` - Name of the real estate project presented via web interface. (Reserved for future use)
 * `class_name` - Name of the class in the new module
 * `active` - (True/False) indicates whether this project is active and should be scraped when `collector` is run.

## Caveats
Curently there is no installer to properly setup all needed files and directories with proper permissions. Following must be manually created.

* log file - This file is defined in config file, `System:logging:file`. If you intend to use file logging you must ensure that this file is writable by user running spoofDog.
* data directory - Spoofdog collects its results into files inside data directory defined in config file, System:data_dir. You must ensure that this directory exists and is writable by user running spoofDog
