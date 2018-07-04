# WOTS
# Word On The Street NLP-Based Real Estate Recommender
WOTS is an NLP-based real-estate recommender designed to help home buyers find their dream home in Seattle and for real estate agents to offer more relatable listings for their clients.

## Why WOTS?
The Seattle housing market continues to grow and real estate companies strive to use data to create more effective listings. Home buyers continue to seek a more advanced method for finding their dream home, beyond basic information such as square footage, number of bedrooms, etc. The WOTS recommender compares listings utilizing the rich text contained in their descriptions and recommends homes of a similar style based upon the buyer's interest. In addition, WOTS compares neighborhoods based on your potential neighbors' reviews and recommends homes of similar style in alternative neighborhoods with a similar vibe.

## Data Source
The neighborhood reviews were scraped from streetadvisors.com and parsed into a Mongo database including the neighborhood name, review, raw html, and url. The real-estate data was provided by flyhomes.com in csv format. In addition to the metadata( number of bedrooms, number of bathrooms, square-footage etc.),the listing dataset contained the geolocations and the text descriptions of the real-estate.

## Data Preparation
The geolocation of the listings were used to identify which neighborhoods they are located in based upon the City of Seattle defined neighborhood boundaries. Results showed inconsistencies between the realtor-defined and city-defined neighborhoods. In addition, a dictionary was created based upon the streetadvisors.com defined neighborhood boundaries so that the reviews can be matched with the listing locations. The common abbreviations ("BR", "BA", "FLR" etc.) in the real estate text description were replaced with the related words ("bedroom", "bathroom", "floor" etc).

## Modeling
The recommender includes two separate data sources: neighborhood reviews and the listing text descriptions. After users input the metadata of number of minimum bedrooms, number of minimum bathrooms, property type, neighborhood and maximum price the model first and finds the matching options within the given neighborhood. Then, based on the selected property:
* The model recommends alternative neighborhoods based on the text similarities of the neighborhood reviews. The model filters each neighborhood review and only keeps the nouns and adjectives of each review using part-of-speech tag functions (pos_tag) from the NLTK library. Then, the model calculates the Term Frequency - Inverse Document Frequency vectors (TF_IDF) for each neighborhood based on the filtered neighborhood reviews. Then model then calculates the cosine similarity for these neighborhoods and finds the top-K most similar options. In the model K is set as 2.
* The model recommends alternative real-estate listings based upon the text description similarities between the selected listing and the remaining listings within both the chosen and model-recommended alternative neighborhoods. Similar to the neighborhood recommender explained above, the model finds top-K real estate listings in each neighborhood based upon the similarities between TF-IDF vectors created using the text descriptions. Since the listing context is specific to the property features, the pos_tag function is not used as a filter.

## Deployment
A webapp was created to show how this model can incorporated into the flyhomes.com website search and help home buyers to find similar listings. This webapp is displayed below.


![](img/wots_record.gif)

![](img/tools.png)
