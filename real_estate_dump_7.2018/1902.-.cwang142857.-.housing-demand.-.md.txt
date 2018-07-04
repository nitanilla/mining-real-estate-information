# Housing Demand
future housing demand projection

# Objective

The goal of this analysis is to project future housing demand in Texas with focus on Houston metropolitan area

# Data
 * Time period: 1998-2016
 * Frequency : monthly
 * Metropolitan Statistical Area (MSA) level:
   * Houston-The Woodlands-Sugar Land, TX
   * Dallas-Fort Worth-Arlington, TX
   * San Antonio-New Braunfels, TX

# Methodology:
  * Quantify housing demand: existing home sales 
  * Features: 
    * label: forward existing home sales
    * features:
       * `employmentTotal_h`: ratio between monthly total empolyment number and history to date average total empolyment per MSA
       * `f1units_r`: ratio between monthly single family building permit and 24 month rolling average single family building permit per MSA
       * `f24units_r`:ratio between monthly 2-4 family building permit and 24 month rolling average 2-4 family building permit per MSA
       * `f5units_h`: ratio between monthly 5+ family building permit and history to date average 5+ family building permit per MSA
       * `hh_inc_h`: ratio between annual household income and history to date average annual household income of Texas
       * `libor12_r`: ratio between average monthly 12m LIBOR and 24 month rolling average 12m LIBOR
       * `months_inventory_g`: monthly YoY change of housing inventory per MSA
       * `oil_p_h`: ratio between monthly WTI price and history to date average WTI price
       * `p_med_h`: ratio between monthly median house price and history to date average median house price
       * `population_h`: ratio between annual population and history to date average population per MSA
       * `unemploymentRate_g`: monthly YoY change of unemployment rate per MSA
       * `wage_growth_r`: ratio between monthly wage growth and 24 month rolling average wage growth of West South Central region
       * `month`: number of month
  * model: ridge regression
 
# Directory

* **raw_data** directory contains all the raw data resources used in this analysis:
  * `sales.xlsx`: monthly MSA level of Sales, Dollar Volume, Average Listing Price, Median Listing Price, Total Listings,	Months Inventory (1990 - 2017)
    * source:   Real Estate Center, Texas A&M University, [website](https://www.recenter.tamu.edu/data/housing-activity/)
  * `dataPermit_full.csv`: monthly MSA level of Building permit data for single-family, 2-4 family and 5-plus family units (1980 - 2017)
    * source:  U.S. Bureau of Census and Real Estate Center at Texas A&M University, [website](https://www.recenter.tamu.edu/data/building-permits/)
  * `dataEmpl_full.csv`: monthly MSA level of Employment and unemployment data (1990 - 2017)
    * source:  U.S. Bureau of Labor Statistics and Real Estate Center at Texas A&M University, [website](https://www.recenter.tamu.edu/data/employment/)
  * `dataPop_full.csv`: annual MSA level of Population estimates and demographic components of change (births, deaths and migration) (1970 - 2016)
    * source:  U.S. Bureau of Census and Real Estate Center at Texas A&M University,[website](https://www.recenter.tamu.edu/data/population/)
  * `household_inc.xls`: annual state level of Median Household Income (1984 - 2016)
    * source: U.S. Bureau of Census, [webiste](https://www.census.gov/topics/income-poverty/income/data/tables.All.html)
  * `wage-growth-data.xlsx`: monthly region level of wage growth rate (1997 - 2017)
    * source: Current Population Survey, Bureau of Labor Statistics, and Federal Reserve Bank of Atlanta Calculations, [website](https://www.frbatlanta.org/chcs/wage-growth-tracker.aspx?panel=1)
  * `libor.csv`: daily level of LIBOR (1986 - 2017)
    * source: Federal Reserve Bank
  * `wti_oil.csv`: monthly level of oil price (1980 - 2017)
    * source: Federal Reserve Bank
  * `Metro_MedianRentalPrice_AllHomes.csv`: monthly metro level of Median price of homes listed for rent on Zillow for All homes (single-family, condominium and co-operative homes) (2010 - 2017)
    * source: Zillow Real Estate Research, [webstie](https://www.zillow.com/research/data/)
  * `Metro_MedianListingPrice_AllHomes.csv`: monthly metro level of Median listing price (or asking price) for homes listed on Zillow for All homes (single-family, condominium and co-operative homes) (2010 - 2017)
    * source: Zillow Real Estate Research, [webstie](https://www.zillow.com/research/data/)
    
* **modeling_data** directory contains the integretated and cleaned dataset for analysis and modeling

* **jupyter notebook** directory contains the jupyter notebook with code and results for presentation


    
    
