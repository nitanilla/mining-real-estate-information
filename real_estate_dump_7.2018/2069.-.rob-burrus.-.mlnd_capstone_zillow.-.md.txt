# MLND Capstone - Zillow

### Overview
This project is a solution to Zillow’s Home Value Prediction competition on Kaggle. The goal is to predict the error in Zillow’s real-estate value predictions. Zillow makes value estimations, called “Zestimates”, for more than 100 million real estate properties in the US. The median margin of error between Zestimate and the actual sales price has dropped from 14% to 5%, making Zillow one of the largest and most trusted sources for real estate information in the US. 

The task is to predict the log-error between the Zestimate and the actual sales price, given the same real-estate features as the Zestimate algorithm. 

## Dependencies

* Python 3
* OpenCV
* Numpy
* matplotlib
* Jupyter Notebook
* CatBoost
* XGBoost

Note: Udacity has a handy Anaconda environment that includes many of the dependencies [here](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md)

## Running the code 
The project is completed in a Jupyter notebook. 
To start Jupyter in your browser, run the following command at the terminal prompt and within your Python 3 environment:

`> jupyter notebook`

* DataExploration.ipynb - zillow dataset exploration
* Preprocessing.ipynb - experimentation with feature engineering and data proprocessing to create training and testing sets
* XGBoost.ipynb - XGBoost model impleementation, testing, and feature analysis
* CatBoost.ipynb - CatBoost model impleementation, testing, and feature analysis

