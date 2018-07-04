##Project 3: Analyzing Real Estate Data | Data Analysis with R

- Author:  Chi-Yuan Cheng (cyuancheng AT gmail DOT com) 
- Last updated: June 25, 2015

### Information

I conducted exploratory data analysis using R to explores the variables, structure, patterns, oddities, and underlying relationships of the residential real estate data  and Census data in USA between 1996 and 2014. 


### Summary

In this project, I did data cleaning, manipulation and analysis using R program. Housing data, Census data and violent crime data from different sources were merged. The main findings are:

1. The sold house price is in overall higher than the listed price.
2. House prices in the West and Northeast are overall higher than these in the North Center and South.
3. House price in USA has a season pattern, with the lower prices in spring and higher prices in summer.
4. Homeowner who has higher income can afford more expensive house and also will pay more house tax.
5. The older people tends to settle in one place for a longer period of time.
6. The crime rate does not strongly correlate to the house price in the state level.

### Data source

- Housing data of USA, 1996-2015, from [Zillow](http://www.zillow.com/research/data/).
    + Median Listing Price per Square Feet
    + Median Sold Price per Square Feet

- US American Community Survey 5 year estimates, 2008-2012.
    + I obtained the Census data by using an API from [US Census Bureau](http://api.census.gov/data/key_signup.html).
    + *To use the API in the R markdown file, your computer need to be internet accessible.*

- Violent crime rates (per 100,000) by state in USA, 1960-2010, from [rMaps](https://github.com/ramnathv/rMaps/tree/master/data). 

###Files

- **Project summary**  ([html](http://rpubs.com/cyuancheng/ZillowHousing) , [Rmd](Project3_RealEstateDataAnalsis.Rmd))   
	includes exploratory data analysis for  residential real estate data  and Census data in USA between 2009 and 2014. 

- **Data files**  
	includes two data files for house price in USA from Zillow.

- **Reference** ([txt](reference.txt))  
	includes reference book and website for this project

- **Certification** ([PDF](certificate-3.pdf))





