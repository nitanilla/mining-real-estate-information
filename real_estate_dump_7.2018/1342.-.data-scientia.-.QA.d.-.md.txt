![Logo](media/qa-d_logo.png)

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Dataset](#dataset)
- [Examples](#examples)
- [Command_line](#command_line)
- [Acknowledgments](#acknowledgments)

## Introduction

<p align="center">

  <img src="https://img.shields.io/badge/bash-4.4.12-blue.svg">
  <img src="https://img.shields.io/badge/zenity-3.24.0-green.svg">
  <img src="https://img.shields.io/badge/whiptail-0.52.18-yellow.svg">
  <img src="https://img.shields.io/badge/powered%20by-jekyll-red.svg">

</p>

QA.d (**Q**uantitative **A**nalysis **d**ataset) is a bash script to automatically download historical stock data from [Yahoo! Finance](https://login.yahoo.com/config/login?.intl=ca&.lang=en-CA&.src=finance&.done=https%3A%2F%2Fca.finance.yahoo.com%2F)  and format it as CSV file. It can run as command line or with GUIs options. You can configure your dataset (in the extent of what's available on Y!Finance).

This program was made as *a learning instrument* for bash scripting; dialogs creation with zenity/whiptail; Github, Jekyll and the projet/kanban board functionality.

The datasets created with this program can be of a sizable amount. If you take all Canadian and American stocks without exclusion (debentures, warrants, preferred shares, etc.) you could get approximately 2Gb to 5Gb of data.

## Features

* Easily create variable size datasets **for free**
* Personalize your historical stock datasets
* Almost no dependencies, packages are default
* The GUI follows your personnal Linux theme
* A '*non graphical*' version is also available
* Who knows? You could become a millionnaire using your dataset to make financial decisions

## Installation

The program has been developed and tested on [Ubuntu 17.10 Desktop](https://www.ubuntu.com/download/desktop) and Linux on Windows 10 pro. The following packages are used by the script. Usually default install on Ubuntu.

You'll need to have an account on Y! Finance to be able to download the data.
* [Yahoo! Finance Account](https://login.yahoo.com/config/login?.intl=ca&.lang=en-CA&.src=finance&.done=https%3A%2F%2Fca.finance.yahoo.com%2F)

| packages | description | explanation |
|--|--|--|
| awk 4.1.4 | GNU awk, a pattern scanning and processing language | only tested on this version |
| bash 4.4.12 | GNU Bourne Again SHell | you need a new version because of the use of ```readarray``` |
| bc 1.06.95 | GNU bc arbitrary precision calculator language | only tested on this version |
| wget 1.19.1 | retrieves files from the web | note that wget handles stuff with the cookies |
| whiptail 0.52.18 | Displays user-friendly dialog boxes from sh | only tested on this version |
| zenity 3.24.0 | Display graphical dialog boxes from shell scripts | only tested on this version |

To validate that you have the prerequisites:
```bash
dpkg -l bash bc gawk wget whiptail zenity
```

You'll get a similar return:
```bash
||/ Name        Version          Architecture     Description
+++-===========-================-================-===================================================
ii  bash        4.4-5ubuntu1     amd64            GNU Bourne Again SHell
ii  bc          1.06.95-9build2  amd64            GNU bc arbitrary precision calculator language
ii  gawk        1:4.1.4+dfsg-1   amd64            GNU awk, a pattern scanning and processing language
ii  wget        1.19.1-3ubuntu1. amd64            retrieves files from the web
ii  whiptail    0.52.18-3ubunt   amd64            Displays user-friendly dialog boxes from sh
ii  zenity      3.24.0-1         amd64            Display graphical dialog boxes from shell scripts
```

## Dataset

As a data scientist, enthusiast or student having full knowledge of your dataset is important. The dataset created by QA.d could be described as:

- Data source : Yahoo! Finance Canada;

- Prices are described at the 6th decimal point;
- Prices currency is CAD$;
- Date field is formated as : ```YYYY-MM-DD```;
- Columns headers are stripped from the dataset;
    - Insert ```TICKER,DATE,OPEN,HIGH,LOW,CLOSE,ADJ_CLOSE,VOLUME``` in first row if needed;
- Off-trading days (stock markets closed) don't appear in the file;
- The best data resolution offered by Y!Finance is *Daily Freq*;
- Line feed is Unix '\n';

Raw content example :
```
ZOM.V,2017-12-01,3.000000,3.100000,2.750000,2.750000,2.750000,51200
ZOM.V,2017-12-04,3.000000,3.000000,3.000000,3.000000,3.000000,1000
ZOM.V,2017-12-05,3.000000,3.000000,2.400000,2.450000,2.450000,12800
ZOM.V,2017-12-06,2.940000,2.950000,2.710000,2.750000,2.750000,7100
```

Formated content example:

| TICKER | DATE       | OPEN     | HIGH     | LOW      | CLOSE<sup>1</sup> | ADJ CLOSE<sup>2</sup> | VOLUME |
| -----  | -----      | -----    | -----    | ------   | ------            | ------                | -----  |
| ZOM.V  | 2017-12-01 | 3.000000 | 3.100000 | 2.750000 | 2.750000          | 2.750000              | 51200  |
| ZOM.V  | 2017-12-04 | 3.000000 | 3.000000 | 3.000000 | 3.000000          | 3.000000              | 1000   |
| ZOM.V  | 2017-12-05 | 3.000000 | 3.000000 | 2.400000 | 2.450000          | 2.450000              | 12800  |
| ZOM.V  | 2017-12-06 | 2.940000 | 2.950000 | 2.710000 | 2.750000          | 2.750000              | 7100   |

<sup>1 Close price adjusted for splits. </sup>

<sup>2 Adjusted close price adjusted for both dividends and splits. </sup>


## Examples

I used the *TSX.ini* (provided in /examples) with a ```Start Date``` of 1971 and got a 251M dataset containing 3,744,812 records on 1489 stocks. My runtime was 24 minutes for which half (~13 minutes) was for ```sleep```. I would not recommend removing the ```sleep 0.5``` in the loop since you could get IP/hostname/username blocked.

The QAd_dataset.csv provided in the /examples shows what the dataset looks like. 

I'm providing some Stocks.ini files for testing:
- Test_mini.ini         (67 random stocks from TSX)
- Test_medium.ini       (314 random stocks from TSX)
- TSX.ini               (1489 stocks from the TSX)
- TSXV.ini              (1522 stocks from the TSX Venture)
- TSX_TSXV_complete.ini (3011 stocks from TSX and TSXV)

**Stock types excluded from the files**

My Stocks.ini files exclude most exotic tickers like ".PR." ".F." ".WT." ".DB." and should include all "common stocks" for their relative stock exchanges. I do not provide support on those files but feel free to add better ones if you have.

I won't explain here what are these types of stocks but you can read [this page on Investopedia](https://www.investopedia.com/university/stocks/stocks2.asp) for more information.

| Ticker code | Describes                    | Status   |
| ----------- | ---------------------------- | -------- |
| .UN.        | Real estate investment trust / Income Fund | Included |
| .PR.,PF,PS  | Preferred shares             | Excluded |
| .WT.        | Warrant                      | Excluded |
| .NT.        | Notes                        | Excluded |
| .A.         | Class                        | Included |
| .B.         | Class                        | Included |
| .C.         | Class                        | Included |
| .D.         | Class                        | Included |
| .F.         | Founders                     | Excluded |
| .L.         | Legended                     | Excluded |
| .N.         | Subscription Receipts 2nd iss| Excluded |
| .R.         | Subscription Receipts        | Excluded |
| .U.         | USD$                         | Excluded |
| .X.         | Class                        | Excluded |
| .Y.         | Redeemable commons           | Excluded |
| .DB.        | Debentures                   | Excluded |


## Command_line

The command line script don't ask for a start date. This is because the ```START DATE``` is always *GMT: Friday, January 1, 1971 12:00:00 AM* and the ```END DATE``` is *Today at midnight* thus downloading a full history for your Stocklist file. There's a sleep timer of 0.5 second between downloads which I find from experience does not lock my IP out of Yahoo.

Usage of the command line script (*QAd_terminal.sh*) is:
```bash
$ ./QAd_terminal.sh "'user@yahoo'" "password" /path/to/Stocklist.ini
```

Output looks like the following:
```bash
user@localhost:/github/data-scientia/QA.d $ ./QAd_terminal.sh "'user@yahoo'" "password" TSX_clean.ini

==================================================================================
QA.d downloader 1.3 -- Your dataset file is: QAd_dataset-20180403.csv
QA.d downloader 1.3 -- Your parameter file is : TSX.ini
==================================================================================

Downloading data for:  AAB.TO
Downloading data for:  AAR-UN.TO
            [...]
Downloading data for:  PSA.TO
Downloading data for:  PSB.TO
            [...]
Downloading data for:  ZYME.TO
Downloading data for:  ZZZ.TO

==================================================================================
Download completed. Historical financial information for 1489 stocks.
File name is : QAd_DATA-20180403.csv File has 3744812 lines for a size of 251M
Runtime was  1431  seconds.
==================================================================================
```

## Acknowledgments

This program was created as a simple exercise to practice bash with zenity.
Most zenity features are tested in this script.
This was created from scratch without researching other programs would could do the same (if my code looks like something else - that's a random occurence).
