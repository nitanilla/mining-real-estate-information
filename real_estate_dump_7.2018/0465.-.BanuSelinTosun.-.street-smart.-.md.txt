# STREET SMART
# Maximize Your Family's Real Estate Investment

### A Zipcode Recommender in Seattle city for Real-Estate: http://www.street-smart-realty.com/

Seattle Real-Estate Market is booming and will continue to grow.
Living on rent is good, but buying a house is a better investment.
What are criteria for this best investment? How can you decide on the best option for what your money's worth?
You may want to consider the schooling options as well.

<img alt="Seattle_RE_Last10Years" src="./img/Seattle_RE_Last10Years.png" height="350" width="700" />

Here, with this app, you can find min/max housing estimates for each Zipcode and the public school ratings with respect to the assigned districts, and a comparison of the private schooling cost with respect to each kids age in the household. And, it is ok if you planning to have kids x many years down the road, the private schooling calculation captures it all...

<img alt="App_Video" src="./img/2017_09_18_212826.gif" height="500" width="1000" />

## Data Collection:
Main data sources are:
* King County
* Seattle Public Schools
* GreatSchool.com
* Zillow

QGIS is used for associating the parcel numbers to public school districts.

![Dataset](./img/BuildingTheDataset.png)

Elementary, Middle, and High School Zones respectively

<img alt="ES Zones" src="./img/ES_Districts.png" height="300" width="200" /> <img alt="MS Zones" src="./img/MS_Districts.png" height="300" width="200" /> <img alt="HS Zones" src="./img/HS_Districts.png" height="300" width="200" />

Sample parcel allocation to HS District: This example is using Ballard High School

![Ballard](./img/Example_Parcel_HS_District.png)

## Data Cleaning:
Classic Feature Engineering methods are applied.
* Data is limited to 100,000.0$ and 2,000,000.0$ for the general purpose of the problem.
* To consider only single-family houses, the living number of units are filtered to 2.
* For the reliability of the model, the data prior to 1985 is discarded.

![Seattle_Real_Estate_Historical_Data](./img/Seattle_Real_Estate_Historical_Data.png)

## Modelling:
Various regressors methods, with GridSearch of respective hyper-parameters, are screened: which are Random Forest Regressor, Gradient Boosting Regressor, Elastic Net CV, Linear and Polynomial Support Vector Regressors, and Linear Regression. Among these, the best results are achieved using Random Forest Regressor with 12.27% median absolute percent error and Gradient Boosting Regressor with 11.30% median absolute percent error. This is also included in the codes, and the jupyter notebooks. Zillow's current median absolute percent error is 5.4 % for Seattle city.

Below is the Residuals Plot: x-axis representing the log of true real-estate cost, y-axis is the log of the ratio of the predicted real-estate cost to true real-estate cost.

<img alt="Tools" src="./img/ResidualsPlot.png" height="300" width="450" />

The feature importance concluded that, not surprisingly, the age of the transaction and sq ft of living are the most crucial parameters. Interestingly, the high school rating is also listed in the three features that decides on the real-estate cost over 80 features considered during modelling. The top ten are shown below:
<img alt="Tools" src="./img/Zoomed_FeatureImportance.png" height="650" width="450" />

The tools used in this projects are listed below, but limited to:
<img alt="Tools" src="./img/ToolBox.png" height="300" width="750" />

## How to make the app work:

The app is live here: http://www.street-smart-realty.com/.

### Please follow the directions below for having the app working in your local browser.

Please download the EXTR_ResBldg.csv and EXTR_RPSale.csv from http://info.kingcounty.gov/assessor/DataDownload/default.aspx
and Residential_Building.zip and Real_Property_Sales.zip files, respectively into the data folder.

Later, run the Feature_Engineering_Functions.py, Parcel_w_ES_MS_HS_Districts.py, School_Ratings.py , and SalePrice_Modelling.py python files in the given order from src directory.

When you run the app.py python file (e.g. "python app.py" from src directory) in your terminal, you will get the html for the application which shows you the predicted housing prices for the given SqFt and number of Bedrooms in each Zipcode with the Public School Ratings, and a comparison of Private School Cost until Collage.
