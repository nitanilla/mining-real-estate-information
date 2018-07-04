# Analysis of real estate market in Singapore with Python

Analysis of Singapore real estate market in the period: July 2015 to July 2016. Data contains real estate prices (from actual transactions) for the several selected districts of Singapore. It is obtained from the [Urban Redevelopment Authority](https://www.ura.gov.sg/uol/ "Urban Redevelopment Authority of Singapore") of Singapore. Analysis is carried out in Python.

![alt text](images/singapore.jpg "Downtown Singapore")

Following Python packages have been employed: `Numpy, Scipy, Pandas, Seaborn, Folium, Scikit-learn, TensorFlow`.

Analysis features exploration of the dataset of actual real estate transactions, using `pandas`, `seaborn` and `folium`. Real estates are geolocated and presented on an interactive folium map. Analysis of real estates, based on their distance from the Metro stations, using data from [MyTransport Singapore](https://www.mytransport.sg/content/mytransport/home.html), is provided. A simple attempt at using a Machine Learning to predict unit prices (in $ per square meter) for real estates, based on the features found in the dataset, is provided as well.

The Jupyter Notebook can be seen rendered on nbviewer [here](https://nbviewer.jupyter.org/github/sarajcev/singapore/blob/master/singapore.ipynb)
