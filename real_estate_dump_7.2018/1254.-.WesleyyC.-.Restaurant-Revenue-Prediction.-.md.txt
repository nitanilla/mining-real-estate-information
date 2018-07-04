# Kaggle: Restaurant Revenue Prediction

Competition Detail: https://www.kaggle.com/c/restaurant-revenue-prediction

Write-Up: https://docs.google.com/document/d/1KU-uzsLLz53S7SwKKnEjk6olbyGaEYRHjF-zv-5HuMk/edit?usp=sharing

Author: Ari Ben-Elazar, Will Burstein, Wesley Wei Qian 

### Final Rank

Rank: 38th/2256 (<2%)

### Approach Records

The models we build is seperated by folders, more detail will come soon.

### Data Description
#### File Description
- train.csv: the training set. Use this dataset for training your model. 
- test.csv: the test set. To deter manual "guess" predictions, Kaggle has supplemented the test set with additional "ignored" data. These are not counted in the scoring.
- sampleSubmission.csv: a sample submission file in the correct format

#### Field Description
- Id : Restaurant id. 
- Open Date : opening date for a restaurant
- City : City that the restaurant is in. Note that there are unicode in the names. 
- City Group: Type of the city. Big cities(class "1" in our processed data), or Other(class "0" in our processed data). 
- Type: Type of the restaurant. FC: Food Court(class "2" in our processed data), IL: Inline (class "1" in our processed data), DT: Drive Thru(class "3" in our processed data), MB: Mobile(class "4" in our processed data)
- P1, P2 - P37: There are three categories of these obfuscated data. Demographic data are gathered from third party providers with GIS systems. These include population in any given area, age and gender distribution, development scales. Real estate data mainly relate to the m2 of the location, front facade of the location, car park availability. Commercial data mainly include the existence of points of interest including schools, banks, other QSR operators.
- Revenue: The revenue column indicates a (transformed) revenue of the restaurant in a given year and is the target of predictive analysis. Please note that the values are transformed so they don't mean real dollar values. 
