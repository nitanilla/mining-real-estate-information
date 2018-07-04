## ACS explorer, cli

A small utility to examine the metadata of ACS tables and vars.

The ACS is a survey of United States demographics run by the Census Bureau. [American Community Survey](https://www.census.gov/programs-surveys/acs/)

You can search for a particular table using the `search` subcommand. Currently, the search is fulltext on table names and table id (not including prefix or suffix), and matching on whole words.

When fetching information about a particular table (the `describe` subcommand), the result will show not only the table and columns (vars), but also every instance of that table over the years, as well as all years the table is available for and which estimate.

In the future, I may implement a feature to allow direct selection of a table from the results of the `search` command. For now, copy and paste from `search` to `describe` is your friend.

## Installation

The acs explorer is written in rust. Currently, the only way to install is to build from source, so you must have Rust installed. I suggest [Rustup](https://rustup.rs). Then:

```
$ git clone https://github.com/hwchen/acs-explorer.git
$ cd acs-explorer && cargo install
```

The first time running, you need to initialize the database and refresh the data. If you miss this step and try `search` or `describe`, it should give you a prompt to initalize anyways.

```
$ acs-explorer refresh
```

## Usage
```
USAGE:
    acs-explorer <SUBCOMMAND>

FLAGS:
    -h, --help       Prints help information
    -V, --version    Prints version information

SUBCOMMANDS:
    search      fulltext search for an acs table
    describe    Get information about a specific table
    refresh     refresh all years and estimates of acs data summaries
    help        Prints this message or the help of the given subcommand(s)

fulltext search (`search` table subcommand):
    - Currently implemented to use exact match.
    - Case insensitive.
    - Searches table name, and table id (no prefix or suffix). 
```

Note that `search` and `describe` have aliases `s` and `d`.

## Examples

```
$ acs-explorer describe B25102

Table Columns:
============================================

code | label      (Year: 2009)
-----+------------------------------------
001  | Total
002  | With a mortgage
003  |     Less than $800
004  |     $800 to $1,499
005  |     $1,500 or more
006  |     No real estate taxes paid
007  | Not mortgaged
008  |     Less than $800
009  |     $800 to $1,499
010  |     $1,500 or more
011  |     No real estate taxes paid
------------------------------------------

code | label      (Years: 2010-2016)
-----+------------------------------------
001  | Total
002  | With a mortgage
003  |     Less than $800
004  |     $800 to $1,499
005  |     $1,500 to $1,999
006  |     $2,000 to $2,999
007  |     $3,000 or more
008  |     No real estate taxes paid
009  | Not mortgaged
010  |     Less than $800
011  |     $800 to $1,499
012  |     $1,500 to $1,999
013  |     $2,000 to $2,999
014  |     $3,000 or more
015  |     No real estate taxes paid
------------------------------------------

Table Information:
============================================

B25102 | MORTGAGE STATUS BY REAL ESTATE TAXES PAID

ACS 5-year estimate: [2009, 2010, 2011, 2012, 2013, 2014, 2015]
ACS 1-year estimate: [2012, 2013, 2014, 2015]
```

```
$ acs-explorer search housing
B00002    | Unweighted Sample Housing Units
B25001    | Housing Units
B25008    | Total Population in Occupied Housing Units by Tenure
B25010    | Average Household Size of Occupied Housing Units by Tenure
B25026    | Total Population in Occupied Housing Units by Tenure by Year Householder Moved Into Unit
B25033    | TOTAL POPULATION IN OCCUPIED HOUSING UNITS BY TENURE BY UNITS IN STRUCTURE
C25033    | TOTAL POPULATION IN OCCUPIED HOUSING UNITS BY TENURE BY UNITS IN STRUCTURE
B25047    | PLUMBING FACILITIES FOR ALL HOUSING UNITS
B25048    | PLUMBING FACILITIES FOR OCCUPIED HOUSING UNITS
B25051    | KITCHEN FACILITIES FOR ALL HOUSING UNITS
B25052    | KITCHEN FACILITIES FOR OCCUPIED HOUSING UNITS
B25075    | Value for Owner-Occupied Housing Units
C25075    | Value for Owner-Occupied Housing Units
B25076    | Lower Value Quartile (Dollars) for Owner-Occupied Housing Units
.
.
.

```
