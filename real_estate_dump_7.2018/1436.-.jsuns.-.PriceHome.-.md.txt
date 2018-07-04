# PriceHome

## Summary

During the past three years, the low inventory and high demand in San Francisco has lead to a constantly high price increase. On average, there is 15% increase each year on the home market in San Francisco.

PriceHome intends to help whoever wants to buy a home in San Francisco to predict the market value of a new listing. PriceHome used machine learning approach combining K-Nearest Neighbors, Binary Space Partitioning, Gradient Boosting, Natural language Processing methods to accomplish this task.

## Data Pipeline
![data pipeline](readme/data_pipe.png)

### Data Source
I collected data by two means:
* Downloading csv files from redfin.com, which includes basic listing information such as last sale price, number of beds, number of baths, SQFT, lot size, parking information, years of built, etc.

* Scraping redfin home page to get description, listing date, HOA amount, homestyle, transportation, and shopping information.

Originally, I collected six month data from May 2015 to Oct 2015 with 2389 homes in San Francisco. The whole data set includes 18527 homes during the past three years (Oct 2012 to Oct 2015).

I used clean.py to clean and prepare data.

### Featurization
To predict the price, I used Median Neighbors Price to approximate the way how real estate agents do in real life. I also added basic listing information as features (SQFT, lot size, parking information, years of built, HOA amount, home style etc). In addition, I extracted four latent features from listing descriptions to capture more information about a listing.

#### Median Neighbors Price
I used K-Nearest Neighbors algorithm to find the k nearest neighbors, and calculated the median price. Finding the geographically closed comparable listings to any given listing involves computationally expensive calculation. I adopted KD-Trees to recursively partition the dataset by latitude and longitude before doing the search.

#### Latent Features
I vectorized the descriptions of the listings with TF-IDF, then used Non-Negative Matrix Factorization to get four latent features and incorporated them into my models.

## Models
I compared random forest, linear regression and gradient boosting and found gradient boosting performed the best.
I did five different models in my study, and compared the results of each model. For six month data, I used 70/30 train-test split to evaluate my models. For three years data, I used the first two and half years data for traning and the last six month data for testing.
![model](readme/model.png)
The most important features are:
* SQFT
* Basic information about a listing (latent feature)
* Building age
* Days on market
* Amenities (latent feature)
* Location (latent feature)
* HOA
* Lot size
* Number of beds
* Number of baths


## Possible future work
* Extract more features from web page (school information, more interior information)
* Personalize the model by zip codes
* Create a web app to predict price for user input listings



## Libraries Used
* Numpy
* Pandas
* scikit-learn
* matplotlib
* seaborn
* BeautifulSoup
* NLTK




