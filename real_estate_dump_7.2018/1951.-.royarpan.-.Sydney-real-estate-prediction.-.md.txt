# Sydney-real-estate-prediction

This repository contains code that uses simulated data to predict the average price of real estate in Sydney suburbs for 2017, 2018, 2022 (5 years) and 2027 (10 years). For our purposes, I compute these prices for 3 Sydney suburbs: North Ryde, North Sydney and Parramatta.

Build environment: Python 2.7 with numpy, scipy, pandas and scikit-learn libraries on Windows, Linux or OS X

Build command: python realestatepredictor.py

Edit line 7 and 8 of code in realestatepredictor.py to initialize data, in line 7 add s=suburb name (e.g., "Parramatta"), in line 8 add the line=line of data from realestatedata.txt for that suburb)

Short description of code: 
My python code uses the median real estate price of houses and units of each suburb for 2015. It builds a Gaussian distribution for year-on-year growth percentage of real estate prices (based on data available for mean year-on-year growth and its standard deviation in 2015). It draws samples from the Gaussian distribution for growth values and creates data points for house and unit prices for the past 100 years. The code then considers two features: 1) number of people employed in the area and 2) walkability score of the area. These features directly affect the housing prices. It computes the values of these two features for the past 100 years for each suburb. The data points thus generated is treated as input (X) to a linear regression model. The output (Y) of the model are real estate prices in 1000$. I create a linear regression model (from scikit-learn library) each for house and unit prices. The coefficients are computed for the linear regression model that best fits this data. Prediction accuracy is computed over a cross-validation set. These coefficients are then used to make predictions for future house and unit prices (based on synthetic test set of feature values for number of people employed and walkability score of each suburb over the next 12 years). The application workflow is depicted in the application workflow diagram.png.
