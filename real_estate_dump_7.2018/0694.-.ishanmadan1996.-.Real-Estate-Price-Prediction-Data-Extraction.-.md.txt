# Real Estate Price Prediction

A web portal that makes use of machine learning techniques to predict housing prices in Mumbai (Central and Western lines). The prediction is based on actual listings obtained from 99acres.com. The selling prices of properties are predicted based on features like location, area, number of bedrooms, furnishing, parking, etc. In order to select a prediction method, various regression methods were explored and compared. Decision tree regression was chosen as it has the advantages of fast training time, higher accuracy and can handle missing values.

## Extracting the data from https://www.99acres.com/

Clone the repository:

```
git clone https://github.com/ishanmadan1996/Real-Estate-Price-Prediction-Data-Extraction.git
```

Install the pre-requisite libraries:

```
pip install requirements.txt
```

Run the Python script for data extraction using:

```
python Data_Extraction.py
```

For cleaning the data to comply with the machine learning model, run the data cleaning script using:
```
python Data_Cleaning.py
```

## Built With

* [Python](https://www.python.org/doc/) - The scripting language used

## Authors

* **Ishan Madan** - (https://github.com/ishanmadan1996)
* **Prathamesh Kumkar** - (https://github.com/iPrathamKumkar)