## Zillow Prize: Zillow’s Home Value Prediction (Zestimate)

### Kaggle competition

“Zestimates” are estimated home values based on 7.5 million statistical and machine learning models that analyze hundreds of data points on each property. And, by continually improving the median margin of error (from 14% at the onset to 5% today), Zillow has since become established as one of the largest, most trusted marketplaces for real estate information in the U.S. and a leading example of impactful machine learning.

### Required libraries
- numpy
- seaborn
- pandas
- matplotlib
- sklearn
- xgboost

### Algorithm

First remove outliers.
Gradient boosting (XGboost) with some unrelated features dropped.
Use L1 and L2 regularization and sub-sample method to reduce overfitting.

### Result

0.06463 mean absolute error, top 46% on Kaggle leaderboard.

### Reference

[Kaggle](https://www.kaggle.com/c/zillow-prize-1)