# Boston Housing Price Prediction

<p align ="center">
<img src = "http://media.bizj.us/view/img/2122231/house-for-sale*750xx1200-675-0-63.jpg">
</p>

#### Project Description

- The Boston housing market is highly competitive, and the goal is to be one of the best real estate agents in the area. To compete in the real estate market, a few basic machine learning concepts are applied in order to assist a client with finding the best selling price for their home. The Boston Housing dataset which contains aggregated data on various features for houses in Greater Boston communities, including the median value of homes for each of those areas. The objective is to build an optimal model based on a statistical analysis with the tools available and then utilize this model to estimate the best selling price for the client's home. Additional information on the Boston Housing dataset can be found [`here`](https://archive.ics.uci.edu/ml/datasets/Housing). The source code developed for this project can be found in the ipython notebook: [`boston_housing.ipynb`](https://github.com/Tsmith5151/Boston-Housing-Price-Prediction-/blob/master/boston_housing.ipynb)

#### Software and Libraries
- Python 2.7
- NumPy
- scikit-learn
- iPython Notebook

### Statistical Analysis and Data Exploration
#### Using the NumPy library, calculate a few meaningful statistics about the dataset:
  
- The following code performs several statistical calculations on the dataset.

```python 
def explore_city_data(city_data):
    """Calculate the Boston housing statistics."""
    number_houses = housing_features.shape[0] # size of data
    number_features = housing_features.shape[1] # number of features
    min_price = np.min(housing_prices) # minimum price
    max_price = np.max(housing_prices) # maximum price
    mean_price = np.mean(housing_prices) # mean price
    median_price = np.median(housing_prices) # median price
    std_price = np.std(housing_prices) # standard deviation
```  
|Statistics          | Value    |
| -------------      | ---------|
| Number of Houses   | 506      |
| Number of Features | 13       |
| Min Price          | $5,000   |
| Max Price          | $50,000  |
| Mean Price         | $22,533  |
| Median Price       | $21,200  |
| Standard Deviaton  | $9,188   |



### Results
####  Based on the developed model, what is the best selling price for your client's home? 

- Once the model has been trained and tested using the methods discussed above, we can now predict the housing price on the out-of-sample data provided by the client as shown in the table below. Statistical analysis performed on the dataset indicates the median home value is `$21,200` and the standard deviation is `$9,190`. Using the out-of-sample data, the model is predicting the average price of the home to be `$21,629`. Being the predicted value falls within one standard deviation of the mean, therefore the predication is considered to be reasonable. The source code can be found in `boston_housing.ipynb` along with further analysis. 


|Features | Sample      |
| --------| ----------- |
| CRIM    | 11.95       |
| ZN      | 0.00        |
| INDUS   | 18.10       |
| CHAS    | 0.00        |
| NOX     | 0.6590      |
| RM      | 5.6090      |
| AGE     | 90.00       |
| DIS     | 1.385       |
| RAD     | 24.0        |
| TAX     | 680.0       |
| PTRATIO | 20.20       |
| B       | 332.09      |
| LSTAT   | 12.13       |


#### Appendix:
   - CRIM     per capita crime rate by town
    - ZN       proportion of residential land zoned for lots over 25,000 sq.ft.
    - INDUS    proportion of non-retail business acres per town
    - CHAS     Charles River dummy variable (=1 if tract bounds river;0 otherwise)
    - NOX      nitric oxides concentration (parts per 10 million)
    - RM       average number of rooms per dwelling
    - AGE      proportion of owner-occupied units built prior to 1940
    - DIS      weighted distances to five Boston employment centres
    - RAD      index of accessibility to radial highways
    - TAX      full-value property-tax rate per $10,000
    - PTRATIO  pupil-teacher ratio by town
    - B        1000(Bk - 0.63)^2 where Bk is the proportion of blacks by town
    - LSTAT    % lower status of the population
    - MEDV     Median value of owner-occupied homes in $1000's
