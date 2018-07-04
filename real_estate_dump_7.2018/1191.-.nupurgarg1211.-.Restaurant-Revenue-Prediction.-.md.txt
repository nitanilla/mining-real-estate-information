### Hotel-Revenue-Prediction
Machine learning project

Kaggle.com - Restaurant Revenue Prediction
Predict annual restaurant sales based on objective measurements Competition Link:https://www.kaggle.com/c/restaurant-revenue-prediction


##Getting Started :

  * Install R 


  * Install RStudio http://www.rstudio.com/products/rstudio/download/
  
##About the Data :
  * Data Set Link: https://www.kaggle.com/c/restaurant-revenue-prediction/data
  * Training data : 137 records
  * Testing data : 100000 records
  * Data Fields :
    * Id
    * Open Date
    * City
    * City Group : Big City , Other
    * Type : FC (Food Court) , IL (Inline), DT (Drive Thru), MB (Mobile)
    * P1, P2 - P37: Three categories of obfuscated data: Demographic data, Real estate data, and Commercial data.
    * Revenue : To be Predicted.

##Data Preparation :
  * Revenue of restaurant in a particular year depends on duration since the restaurant opened.Hence, we extracted number of days from “Open Date” attribute.As expected, for most of the rows, we found high correlation between the revenue of the restaurant and the number of days since it had opened. Although we found a few outliers, we decided to keep this column for further analysis
  * Comparison of records of various cities.
    Testing Data  vs. Training Data
    We can observed that Istanbul(Big city) has comparatively very high restaurants. Also,there are 34 cities in training       data and 57 cities in testing data. Hence, City name is not a predictor.
    So, we converted all the Big cities to “Istanbul” and named all Small cities to “Other”. This was
    done in both training and testing data.
  * There was no “MB” Type is Training Data. So the any model can’t predict for mobile restaurants.
    Hence replaced “MB” with “FC” type.
  * Density plot of revenue v/s Density plot of log(revenue)
    The revenue column in the training dataset had a skewed distribution. A log scaling on the revenue gave a much better       distribution of revenue. Sometimes, predictive models tend to be sensitive to the skewness in data. To guard against        this, we applied a log transform to the revenue column to make it close to a normal distribution.

##Building the Prediction Model :
We first tried using linear regression for generating the prediction model. But, the linear model had a
very high prediction error. Therefore, we chose to move to non-linear regression models. We decided
to go ahead with tree-based approaches for regression. We used Random Forests.It uses an ensemble
of decision trees to predict the final outcome.

##Result and Evaluation :
Our measure of evaluation was private leaderboard score. As the competition is over, as soon as we
upload a solution, we can find public and private leaderboard score. So we considered higher rank as
error measure and use models to improve our rank ( which means decreasing the error).
Our final submission had following ranks :
* Public Leaderboard : 438th Rank
* Private Leaderboard : 35th Rank
We learnt that when training sets are small, performing cross-validation on the training set provides us
with trustworthy error values. There is also risk of overfitting for very small datasets as seen by low
public score but high private score.



