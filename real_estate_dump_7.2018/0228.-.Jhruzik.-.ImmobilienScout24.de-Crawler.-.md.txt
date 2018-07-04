# Crawler for Houses and Flats on https://www.immobilienscout24.de/
This crawler will crawl all the listings for flats and houses (rent and sale) on the German real estate website www.immobilienscout24.de.

### Dependencies
This crawler was programmed with **Python3** and **BeautifulSoup4**. Naturally, you would need to install **Python3** as well as the **BeautifulSoup4** module. Pandas was used for data wrangling and generating the output. I recommend using **Anaconda** which already includes Pandas.

### Usage
By inputing some paramters via your command line (e.g. Bash in Linux or cmd on Windows) you can customize this crawler to your specific needs. The parameters are *--type=* and *--payment=*. *--type=* specifies what sort of real estate you want to crawl. *--type=* accepts either one or both of the letters h (houses) and f(flats). *--payment=* takes either one or both b (buy) or r (rent). In the end, your call should look something like this: `python immoscrap.py --type=hf --payment=br`. This command will crawl houses (h) and flats(f) for rent (r) and sale (b). You could trim your search by inputing fewer search parameters but there must be at least one for both *--type=* and *--payment=*.

1. Make sure that all dependencies are installed.
2. Open a command line terminal.
3. cd into the crawler's directory.
4. type in `python immoscrap.py --type=hf --payment=br` for crawling houses and flats that are for sale and rent. Make adjustments to *--type=* or *--payment=* if you wish.

### Output
The total progress will be printed to the command line while running. In the end, you'll find a new folder called *Results* containing two sub-folders with the names *Raw* and *Clean*. Both folders will contain the data in a .csv file. However, the data in *Raw* is unformatted, while the data in *Clean* is already processed.

### Formatting
German formatting conventions are used. This means that ";" is the delimeter inside the .csv file. Also note that the decimal seperator is equal to "," and not "."! Keep these formatting conventions in mind when you read in the data.

### Usage
Feel free to use this data and crawler for your personal/academic/commerical projects. If you write an academic paper, I would appreciate to be mentioned by my full name (see bio). Please be polite when crawling. This crawler was not developed to do any harm.
