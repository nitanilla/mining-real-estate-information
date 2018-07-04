# Getting Zillow-like Performance with a Subset of the Data: Predicting Boston Area Home Sale Prices Using Only Physical Features

# Abstract

Predicting the sale price of a home is easy when given the entire history of the property including past sale prices, tax assessments, and physical attributes. Take the localized market growth, apply it to the last sale price and tack on any additions or subtractions to credit new features. However predicting the sale price of a home when given only physical attributes is a much harder problem. The regression models are no longer seeded with a known historical baseline - they instead have to look a layer deeper and start attributing features with values, location coordinates with land value, and realtor comments with discrete dollar deltas.

The goal isn't to beat common home valuation tools like Zillow and Redfin at their own game. Instead the goal is to get similar accuracy using a much smaller subset of data for each home, not to mention a much smaller amount of training data. The smaller dependence on data opens more doors as there's no longer a strict dependence on having historical data and tax information. Using only twenty-five features which can easily be specified by a user on a phone we can generate a valuation that's almost as good as one based on myriad data sources and historical data that may or may not be emotionally influenced.

# Table of Contents

- [Introduction](#introduction)
- [Methods](#methods)
  - [The Data](#the-data)
  - [The Models](#the-models)
  - [Iteration 0](#iteration-0)
  - [Iteration 1](#iteration-1)
  - [Iteration 2](#iteration-2)
  - [Iteration 3](#iteration-3)
- [Results](#results)
  - [Scoring](#scoring)
  - [Iteration 0](#iteration-0-1)
  - [Iteration 1](#iteration-1-1)
  - [Iteration 2](#iteration-2-1)
  - [Iteration 3](#iteration-3-1)
- [Discussion](#discussion)
- [Conclusions](#conclusions)
- [Acknowledgements](#acknowledgements)
- [References](#references)



# Introduction

A decade ago the only way to get a trustworthy valuation of your home was to call in a realtor to do a comparative market analysis (CMA). Unfortunately doing a CMA is a lengthy process that can take anywhere from 2 - 8 hours and as such either payment or the promise of business for that realtor is a typical prerequisite. The curious prospective seller wanting to get an idea of the value of their home was limited to the crude methods of scoping out nearby open houses and word of mouth exchanges.

But with the internet revolution came a revolution in home valuation - tools like Zillow's Zestimate started popping up promising to give you an instant valuation of your home from your browser. No realtors, no coy smalltalk with neighbors, no commitment to selling your home - the curiosity of the prospective seller can now be satiated. But just how accurate are these new predictions and what data do they use?

Nationally Zillow manages a median error rate of 7.9% which drops to 7.5% when only considering the Boston area. Of those 1.5 million Bostonian homes - 35.3% of the Zestimates are within 5% of the actual sale price; 62.6% within 10%; 87.8% within 20%; leaving 12.2% that are more than 20% off.


Some of the data that Zillow uses to achieve these estimates are -

  - Physical attributes
    - Location
    - Square footage
    - Number of bedrooms, bathrooms.
    - Etc.
  - Tax assessments
    - Property tax information
    - Actual property taxes paid
    - Etc.
  - Prior history
    - Actual sale prices of the home
    - Comparable recent sales of nearby homes


Another home valuation service Redfin claims to use 500 data points ranging from the neighborhood the home's in to specialized qualitative information like whether the home has a water view or the calculated noise pollution levels. That's all well and good but these models have a high dependence on the availability of this information and they start breaking down when considering brand new homes that have no history or no tax records. That's the scenario that we're going to target. In fact the explicit list of features that we'll consider is below -

  - Address
  - Zip-code
  - Age
  - Square footage
  - Lot size
  - Style
  - Number of bedrooms
  - Number of bathrooms
  - Number of garages
  - Number of floors
  - Number of fireplaces
  - Type of roofing
  - Type of flooring
  - Type of appliances
  - Type of foundation
  - Type of construction
  - Type of exterior
  - Type of insulation
  - Type of water heater
  - Type of heating
  - Type of wiring
  - Exterior features
  - Interior features
  - Basement
  - Realtor remarks

We'll later find that most of these are relatively unimportant features and can be removed without much effect on the accuracy of the model. Regardless they're all specified whenever a home is entered into MLS (multiple listing service) and thus serve a good starting point as every home will have at least these features. It's also a good starting point because it's all information that a home owner should be able to come up with fairly easily if given drop downs of options for each. If made accurate this would open up the world of CMA's and appraisals as they no longer require specialized knowledge but can be performed by the home owner with only a phone.

But the path to accuracy won't be easy. We'll take these 25 features and transform them into over 322 features by geolocating addresses, clustering homes in several dimensions, analyzing the paragraphs of remarks left by realtors, and tuning the hyper parameters of chained models. From that incredible amounts of data we'll generate a single number for every home - our predicted sale price of the home if it was sold today. May the odds be ever in our favor.


# Methods

The project was done with an iterative development model in mind and as such it only makes sense to present the project using it's iterations. The first iterations were primarily dedicated to building out the data pipeline and normalization techniques but also featured crude models based on small subsets of the data. Then the models started getting more refined as more and more features were incorporated into the models via more feature extraction and text analysis. The final iterations had the smallest code delta but took the most amount of time as they were heavy on tuning model hyper-parameters and soaking as much accuracy out from them as possible.


## The Data

The data for 21,657 homes was sourced from the multiple listing service (MLS).

## The Models

We'll talk about a variety of models and algorithms used to form our estimation pipelines. While this paper does expect some level of statistical knowledge; it doesn't make the leap that the reader is familiar with the intricacies of various regression models. As such I wanted to include a brief section dedicated to a quick overview of the models and algorithms that we'll see. Because my primary machine learning library used was scikit-learn - all regressors and algorithms below used the implementation that can be found in that package.

#### Regression

- ##### Random Forests

 A random forest is a meta-estimator formed by an ensemble of decision trees each fitted over different subsamples of the dataset. The output value is then the mean of each decision tree's output values. Random forests are versatile and often the goto model when facing a new problem as they can help uncover the relative importance of features.

- ##### Extremely Randomized Forests

 Functionally equivalent with random forests but introduce more randomness when selecting a subset of features. This tends to reduce the variance of the model in exchange for a slight increase in bias.

- ##### Gradient Tree Boosting  

 Another ensemble method, gradient boosted regression trees form ensembles of weaker decision learners that improve on their predecessor's estimate by chaining a new tree on the error of the last tree.

- ##### Least Angle

 Least angle regression is a linear regression algorithm typically used when overfitting is a concern or when analyzing a sparse matrix.

#### Clustering

- ##### MeanShift

 Mean shift by itself is a technique for locating maximas in a density function. Mean shift clustering works by assuming that the input data is a sampling from an underlying density function. It then uses mean shift appropriately to uncover modes in the feature space (clusters of similar values).

#### Matrix Decomposition

- ##### Truncated Singular Value Decomposition

 Matrix decomposition algorithm used to reduce the dimensionality of an input matrix. In the context that we're using it (word frequency matrices) it's actually called latent semantic analysis.

#### Feature Extraction

- ##### tf-idf

 Term frequency inverse document frequency. This term frequency transformation will reweight the term frequency of a blob by the inverse of the commonality of the term across all blobs. That is, it'll scale down the reported frequencies of common words and scale up the frequencies of unique words. This is a common technique to reflect word importance and help summarize text.


## Iteration 0

Location, location, location. Unfortunately _221B Baker Street_ doesn't give our models much to work with so the first preprocessing step is to geocode our entire suite of testing and training data. The fundamental flaw with an address is that addresses on their own don't contain any proximity information beyond the street name - are _17 Welthfield St_ and _2998 Homer Ave_ close to each other (and thus have similar land value)? It's impossible to say without first converting the address to their geographical coordinates. Suddenly the problem of proximity is reduced to euclidean distance. Geocoding in itself isn't a mystery so I'll skim over the implementation details but the source code can be found in [geocode_data.py](geocode_data.py).

Also in this iteration was the first foray into regressors. The first iteration ended with six distinct regression models with each model using either a different regression algorithm or a completely different subset of the data. Specifically we have -

- Linear Regressor using only the square footage of a home
- Random Forest Regressor using only the location of the home
- Random Forest Regressor using only `LAT/LNG/AGE/SQFT/BEDS/BATHS/GARAGE/LOTSIZE`
- Random Forest Regressor using all but realtor remarks
- Extremely Randomized Trees Regressor using all but realtor remarks
- Gradient Boosted Regression Trees using all but realtor remarks

Worth noting is the heavy reliance on ensemble methods here. An ensemble method (i.e. RFR, ERTR, GBRT above) is an estimator constructed from either averaging methods that average the results of several simpler estimators or boosting methods which construct successive generations of simple estimators each based on the error rate of the previous. The reliance on ensemble methods is because they were quite simply the empirical best. I tried a variety of generalized linear models, support vector machines and decision trees but kept coming back to the ensemble methods.

There's also the small detail I skipped over regarding how I'm incorporating the non-numerical data into my models. Take the 'Hot Water' feature as an example - it's possible values are any combination of the set of options `Electric, Geothermal/GSHP Hot Water, Leased Heater, Natural Gas, Oil, Propane Gas, Separate Booster, Solar, Tank, Tankless, Other`. To handle that I take all categorical features and generate several indicator features, one for every unique category in the feature. The 'Hot Water' feature is thus split into eleven distinct features each containing a binary number for whether or not that specific category within 'Hot Water' is present. Specifically we generate the columns `(Hot Water) electric, (Hot Water) geothermal/gshp hot water, (Hot Water) leased heater, (Hot Water) natural gas, (Hot Water) oil, (Hot Water) other (see remarks), (Hot Water) propane gas, u(Hot Water) separate booster, (Hot Water) solar, (Hot Water) tank, (Hot Water) tankless`.

The unfortunate consequence of this feature extraction is that we start with matrix dimensions `(21657, 20)` and end with matrix dimensions `(21657, 323)`. As we find out later this can almost end up hurting us as highly correlated and valuable features can get lost in the pool of relatively insignificant features.

## Iteration 1

In this iteration we took the best three models from the previous iteration and introduced cross validation, a technique used to minimize overfitting (see [Scoring](#Scoring)). The selected models are below -

- Random Forest Regressor using all but realtor remarks
- Extremely Randomized Trees Regressor using all but realtor remarks
- Gradient Boosted Regression Trees using all but realtor remarks

We then picked the best performing model of the three after cross validation and starting tuning the model's hyperparameters. A hyperparameter of a model are more or less a specific set of constants used in a model that affect the ultimate accuracy of the model. In the case of gradient boosted regression trees the hyperparameters include (list and descriptions courtesy of scikit-learn documentation) -


- ###### loss : {‘ls’, ‘lad’, ‘huber’, ‘quantile’}, optional (default=’ls’)

 loss function to be optimized. ‘ls’ refers to least squares regression. ‘lad’ (least absolute deviation) is a highly robust loss function solely based on order information of the input variables. ‘huber’ is a combination of the two. ‘quantile’ allows quantile regression (use alpha to specify the quantile).
- ###### learning_rate : float, optional (default=0.1)

 learning rate shrinks the contribution of each tree by learning_rate. There is a trade-off between learning_rate and n_estimators.
- ###### n_estimators : int (default=100)

 The number of boosting stages to perform. Gradient boosting is fairly robust to over-fitting so a large number usually results in better performance.
- ###### max_depth : integer, optional (default=3)

 maximum depth of the individual regression estimators. The maximum depth limits the number of nodes in the tree.
- ###### min_samples_split : integer, optional (default=2)

 The minimum number of samples required to split an internal node.
- ###### min_samples_leaf : integer, optional (default=1)

 The minimum number of samples required to be at a leaf node.
- ###### min_weight_fraction_leaf : float, optional (default=0.)

 The minimum weighted fraction of the input samples required to be at a leaf node.
- ###### subsample : float, optional (default=1.0)

 The fraction of samples to be used for fitting the individual base learners. If smaller than 1.0 this results in Stochastic Gradient Boosting. subsample interacts with the parameter - n_estimators. Choosing subsample < 1.0 leads to a reduction of variance and an increase in bias.
- ###### max_features : int, float, string or None, optional (default=None)

 The number of features to consider when looking for the best split:
- ###### alpha : float (default=0.9)

 The alpha-quantile of the huber loss function and the quantile loss function.


While it may seem persnickety to worry about fine-tuning models already, the term 'fine-tune' is perhaps a misnomer. While fine-tuning my models I noticed some configurations which achieved scores significantly above the default but I also achieved scores that were in the single digits. Just by lowering the minimum weighted fraction of samples required to be a leaf I could end up reducing my model accuracy from 0.88 to 0.02. It also means that perhaps the default model isn't performing as well as it can and we may be able to squeeze out a significant bit of accuracy before moving on to more complex additions. There are three primary techniques for tuning the hyperparameters of a model. You can guess, you can try random combinations, or you can try every possible combination. I tried all three.

#### Guessing

There's one variable which guessing works quite well with - n_estimators which is the number of boosting stages to perform. Gradient Tree Boosting is an ensemble method in that it forms ensembles of weaker decision learners, each ensemble improving on their predecessor's estimate by chaining a new tree on the error of the last tree. The number of boosting stages is how many of these improvement stages occur. We can guess this constant because at every iteration if we measure the deviance of both the training set and the testing set and graph this deviance, we can tell when improvement starts slowing down. From there we can select a reasonable trade off between training time and trailing off accuracy improvements.

![Graph of Deviance vs. Iterations](images/figure_1.png)

![Graph of Improvement vs. Iterations](images/figure_2.png)

#### Randomly Guessing

The Python machine learning framework Scikit-learn (colloquially known as 'sklearn') includes a helper module with utilities to fine-tune models. One of these utilities is RandomSearch. In RandomSearch you define distributions or lists of possible values for each parameter. RandomSearch will then run for N iterations, at each iteration randomly selected each parameter, fitting a model with those parameters and scoring the fitted model. After hitting the specified number of iterations it'll then report the best parameter combination it's had so far. While not exhaustive it tends to perform quite well while trying significantly fewer combinations than the next utility, GridSearch.

#### Guessing Everything

Another one of those utilities in sklearn is GridSearch. How GridSearch works is you define a list of possible values for every parameter defining a grid of possible combinations. GridSearch will then iterate over every combination, train your model using that combination of parameters and score it's accuracy. After exhausting the space of combinations it'll then report the top N configurations that produced the highest score. While incredibly useful given a small set of combinations, because of innate combination theory this utility is often time prohibitive when you want to search a large grid of combinations.


## Iteration 2

The iteration of the realtor remarks. Up until now I've been ignoring the realtor's remarks in favor of the hard numerical and categorical data. However now that we've run out of that data we have to turn towards the realtor's remarks in an effort to further improve our model. Typically only a paragraph long, the remarks contain crucial information not mentioned in the other data like proximity to town centers, special features or traits about the home, or even something as subtle yet fiscally significant like 'remodeled kitchen'. Here's a selection of some actual remarks from our training data that we'll be analyzing in this iteration -


> The classic Colonial is prominently sited in popular Patriot Hill neighborhood.  The first floor offers a front to back LR, DR, cherry kitchen and inviting family room with French doors that open to a three-season porch.  Upstairs is the MBR with updated bath, three family bedrooms and bath, and a secluded home office.  The finished lower level offers additional family space.  Highlights include hardwood flooring, new windows and siding plus recent roof and furnace.  Pool available.

---

> An imposing Turn of the century Colonial Revival set back on 1.28 acres on  the Chester Brook . Twelve rooms ,5 bedrooms+,3 fireplaces, 2 full baths, 2 car garage front and back stairways. Wonderful period detail inside and out. Listed on the local historic register as "the Charles Whitney House" and is considered "the city's best example of a cross-gabled gambrel roofed Colonial Revival". Updates will be required to this classic home. All showings require confirmed appointment of 24 hrs.

---

> This classic colonial is conveniently located on a Cul-de-sac in Arlington Heights within a short distance to The Minuteman Bike Path, area amenities, schools, parks, transportation and major routes.  Hardwood floors throughout, crown molding on first floor and bonus walk-up attic.  The light filled first floor bedroom with private full bath can be used as a family room/office.  Recently painted inside and out and updated windows, this home offers a private yard with patio off the kitchen.

---

> A masterpiece of vision,liveability & quality. Holly Cratsley of Nashawtuc Architects in concert with Molly Tee of Deck House designed a one of a kind gem redone in phases to perfection. 2 story atrium foyer. Boston Design Center european kitchen with granite & re-cycling center. Breakfast room with walk- in pantry.peaceful family room. Dramatic 2nd fl.great room. Screened porch. A/C 2nd floor. Partial basement. Pond for swimming, skating,canoeing & neighbors gathering. Hiking trails closeby.


There's a few advanced unsupervised learning methods you can apply to text blob analysis but for the sake of simplicity we'll be sticking to a supervised technique that's ultimately based on word frequency. The first step is to tokenize the strings and break the paragraph into a matrix of word frequencies. Unfortunately word frequencies don't tell us much as well, some words are naturally more common than others. To offset this effect we perform what's called a tfidf transformation (term frequency inverse document frequency) which re-weights every word by the inverse of how common that word is across every other text blob. This way common words like 'the' will have a negligible weight compared with more uncommon words like 'masterpiece'.

One of the problems with this technique is we start to lose meaning as we take words out of context. Take the example string, "Great location, noise levels bad". Using the above technique we'll tokenize the string into the sorted array `['bad', 'great', 'levels', 'location', 'noise']` and then attempt to perform analysis on that array despite that array having lost all contextual meaning. A method of preserving context is instead of splitting based on words why not try splitting on both words and pairs of words? The new array would be `['bad', 'great', 'great location', 'levels', 'levels bad', 'location', 'location noise', 'noise', 'noise levels']` which starts to get across some of the original sentiments better than the single word alternative. My final tuned model took this even further by generating n-grams (contiguous sequence of N words from text) of up to four words long.

Now we have a sparse matrix with size `(21657, 83968)` where each column is a unique word or phrase, each row is a specific home, and each cell contains the tfidf re-weighted frequency of that word/phrase in that home's remarks. But attempting to train a regressor on a matrix this sparse and with this many features will take forever and eat all available memory while it's at it. Instead we'll first pass the sparse matrix through the matrix decomposition algorithm truncated SVD to reduce it to size `(21657, 500)`. While I'm hesitant to get into the details of the latent semantic analysis we're doing here I do want to say that it's a very well known technique of analyzing and representing the contextual based meaning of words and phrases while also reducing matrix dimensionality.

The final step in this pipeline is to perform some form of regression on our matrix. Through extensive empirical testing I found that the ensemble methods I've used previously weren't really delivering a good amount of accuracy with this new set of data. Instead I settled on the linear model of Least-angle regression (LARS) for several reasons: it's fast; it works well with high dimensional data; it reliably performed the best out of all the other linear models.

Also in this iteration were more randomized searches across the space of parameter combinations to tune the tfidf, tsvd, and lars transformations.


## Iteration 3

At this point we've accounted for all the data in either the GBRT or the realtor remarks pipeline. Now all that's left to do is hook the models up to each other in some way so we can aggregate the individual predictions into a more accurate umbrella prediction. To do this and all the intermediate transformations we're utilizing another sklearn utility module that contains Pipelines and FeatureUnions. A pipeline is just as it sounds - a chain of transformers that fit their input and output their transformed input to the next transformer in line. Calling .fit() on a pipeline is equivalent to calling .fit() and then .transform() successively on every transformer in the pipeline. FeatureUnions work in the other dimension and concatenate the outputs of N individual transformers into a single output matrix. Using both pipelines and feature unions allow us to create very complex machine learning pipelines.

But there's one last feature extraction technique left. In the previous few iterations I noticed from outliers that the models aren't attributing the location of a home as strongly as I would like. A two bed two bath home surrounded by several million dollar homes should be worth significantly more than a two bed two bath in a less desirable neighborhood. In an attempt to reinforce localized variances we'll run a subset of the data through a clustering algorithm with the intent of clustering nearby homes that have similar attributes. We'll then include these clusters in our umbrella model in the hopes that it'll recognize wealthier clusters from less appealing clusters and derive some semblance of wealth from the other homes in a cluster.

The clustering technique I've chosen to do so is called MeanShift. Mean shift by itself is a technique for locating maximas in a density function. Mean shift clustering works by assuming that the input data is a sampling from an underlying density function. It then uses mean shift appropriately to uncover modes in the feature space (clusters of similar values). We'll run MeanShift on the subset of features `['lat', 'lng', 'SQFT', 'BEDS', 'BATHS', 'ZIP', 'GARAGE', 'LOTSIZE']` in the hopes of getting clear localized clusters, and possibly separate clusters between the more expensive and less expensive homes in a neighborhood.


We're going to attempt two distinct prediction pipelines -

1. We predict sale price using only remarks. We predict sale price using our best GBRT model which includes all data but remarks and including clusters. We run these two columns of predictions through another regressor to make a third and final prediction using just those two predictions.

2. We predict sale price using only remarks. We concatenate this predicted sale price calculated from remarks with the clusters and append them to the original data set. We then run our best GBRT model over this data set to generate a final prediction.


# Results

## Scoring

We need a method of scoring the accuracy of our regression models and one of the primary ways we're going to do so is the coefficient of determination (R<sup>2</sup>). R<sup>2</sup> has the range [0.0, 1.0] and represents the fraction of variance in the output that's predictable from the input. While generally a good scoring method it does suffer from a few problems like when sample size increases as R<sup>2</sup> rewards larger sample sizes (fixed by adjusted R<sup>2</sup>). An R<sup>2</sup> of 1.0 means that the model is predicting perfectly.

To allow us to compare our regression capabilities to that of Zillow we'll also be looking at the mean absolute percent error in a few cases. MAPE on it's own isn't a very good scoring method as predictions that are systematically low are bounded to a MAPE of 100% while predictions that are systematically too high are unbounded. This means that when using MAPE to compare models there exists a bias towards estimators that predict lower versus models that predict higher. A MAPE of 0.0 means the model is predicting perfectly.

We also face the issue of overfitting. The usual method of dealing with overfitting is handled by segmenting your data into two distinct sets - a training set and a testing set. But this still isn't perfect because when tuning the hyperparameters of models we'll favor the parameters that perform the best on the testing set (but not necessarily new data). To handle this overfitting problem we introduce the idea of cross validation, specifically K-Fold cross validation. K-Fold CV segments the dataset into K distinct but equal subsamples. K-1 of the subsamples are used to train the model and the remaining subsample is then used as the testing data. This is repeated K times so that every subsample has the chance to be the testing set. The resultant score is usually the average of the K subscores.


## Iteration 0

For every model in this iteration we've included both the R<sup>2</sup> score as well as a sample of predictions made. Next to our predicted values are both the list price and the sold price of the respective home which allows us to gauge what an 'acceptable' value is.

##### Linear Regressor using only the square footage of a home
```
          Accuracy: 0.459411179095

          Predicted                    List Price                     Sale Price         
           537,373                        289,500                        295,000          
           788,038                        850,000                        820,000          
           563,946                        449,900                        430,000          
           647,936                        699,900                        660,000          
           588,858                        749,000                        805,000          
           658,257                        585,000                        570,000          
           724,452                        719,900                        708,000          
           677,000                        679,000                        700,000          
           581,266                        465,000                        450,000          
           833,355                       1,058,000                      1,000,000         
           477,465                        349,900                        360,000          
           489,328                        315,000                        295,000          
           536,780                        379,900                        370,500          
           616,262                        549,900                        547,000          
           478,414                        279,900                        273,000          
           532,509                        349,000                        337,000          
           587,079                        443,900                        420,000          
           573,911                        449,900                        455,000          
           680,559                        599,900                        575,000          
           515,426                        339,900                        339,900          
```

##### Random Forest Regressor using only the location of the home
```
          Accuracy: 0.512581201614

          Predicted                   List Price                     Sale Price          
          392,130                        779,000                        816,250           
          463,825                        475,000                        450,000           
          569,080                        589,900                        587,400           
          491,710                        975,000                        950,000           
          286,170                        389,000                        395,000           
          632,695                        319,000                        319,000           
          360,395                        419,900                        408,000           
          610,860                        425,000                        414,000           
          419,760                        519,900                        499,900           
          415,287                        459,900                        460,000           
          445,330                        445,000                        420,000           
          1,437,681                       549,000                        522,000          
          280,043                        249,900                        251,000           
          455,712                        459,900                        420,000
          547,539                        699,800                        665,000           
          867,808                        819,900                        824,723           
          363,740                        339,900                        323,000           
          395,186                        575,000                        555,000           
          921,068                       1,449,000                      1,485,000          
          1,067,873                      1,325,000                      1,210,000
```

##### Random Forest Regressor using only `LAT/LNG/AGE/SQFT/BEDS/BATHS/GARAGE/LOTSIZE`

```
          Accuracy: 0.860120147944

          Predicted                   List Price                     Sale Price    
          437,195                        529,900                        540,000           
          671,328                        589,000                        570,000           
          460,552                        359,000                        360,000           
          409,415                        395,000                        372,000           
          466,588                        595,000                        550,000           
          1,556,137                      1,359,000                      1,320,000         
          761,688                        759,000                        725,000           
          321,212                        419,900                        400,000           
          264,517                        274,900                        276,000           
          373,922                        389,900                        389,000           
          449,084                        479,900                        470,000           
          527,548                        475,000                        465,000           
          375,329                        329,900                        315,000           
          627,696                        699,000                        696,000           
          340,283                        349,900                        356,414           
          442,917                        419,900                        407,000           
          197,086                        275,900                        270,000           
          358,586                        389,900                        389,900           
          476,083                        399,900                        399,000           
          462,015                        429,900                        422,000

```

##### Random Forest Regressor using all but realtor remarks
```
          Accuracy: 0.864045570243

          Predicted                   List Price                     Sale Price    
          393,343                        444,900                        420,000           
          650,725                        649,000                        640,000           
          497,629                        489,000                        482,000           
          644,374                        699,000                        678,000
          448,547                        480,000                        472,500           
          441,195                        489,900                        475,000           
          560,107                        585,000                        578,000           
          853,622                        885,000                        990,000           
          575,484                        598,000                        598,000           
          915,815                       1,250,000                      1,195,000          
          837,188                        899,000                        874,500           
          438,348                        539,900                        530,000           
          680,572                        739,900                        705,000           
          416,549                        335,900                        325,000           
          286,449                        199,900                        187,000           
          786,023                        785,000                        782,000           
          419,564                        519,900                        489,000           
          533,769                        499,900                        492,500           
          404,101                        431,900                        415,000
          387,042                        419,900                        420,000
```

##### Extremely Randomized Trees Regressor using all but realtor remarks

```
          Accuracy: 0.882409157472

          Predicted                   List Price                     Sale Price          
          1,250,428                      1,325,000                      1,325,000         
          528,822                        509,900                        485,800           
          577,275                        610,000                        615,000           
          930,412                        959,000                        958,000           
          692,539                        779,000                        764,500           
          425,572                        499,000                        485,000           
          930,020                        949,900                        890,000           
          513,619                        609,000                        595,000           
          503,727                        450,000                        485,000           
          346,979                        299,900                        299,900           
          457,454                        489,900                        485,000           
          619,712                        599,000                        574,000           
          774,598                        899,900                        875,000           
          287,053                        280,000                        263,000           
          732,971                        689,900                        689,000           
          403,004                        459,900                        435,000           
          395,532                        389,900                        370,000           
          740,589                        699,000                        665,000           
          685,062                        629,000                        635,000           
          269,818                        315,000                        300,500           
```

##### Gradient Boosted Regression Trees using all but realtor remarks

```
          Accuracy: 0.885379973123

          Predicted                   List Price                     Sale Price          
          628,326                        649,000                        649,000           
          1,098,072                       949,999                       1,015,000        
          538,834                        595,000                        595,000           
          624,204                        629,900                        597,500           
          650,419                        675,000                        665,000           
          583,247                        575,000                        580,800           
          688,979                        849,000                        815,000           
          434,513                        495,000                        480,000           
          645,526                        729,000                        750,000           
          567,911                        489,000                        481,500           
          577,030                        479,900                        490,000           
          375,504                        389,900                        385,000           
          366,270                        399,000                        375,000           
          493,915                        599,000                        662,000           
          1,417,576                      1,848,000                      1,902,000        
          464,973                        529,000                        523,500           
          320,100                        319,900                        317,500           
          263,166                        279,900                        277,000           
          635,963                        799,900                        765,000           
          953,021                        899,900                        893,000           
```

Judging purely by score the final model using the boosting technique on our entire set of data minus realtor remarks seems to be the most accurate (we'll incorporate the remarks in a later iteration). As you can see in the sample of predictions made there are several cases where the prediction is eerily accurate and gets within $10,000 of the final sale price but there's also a fair share of predictions as far off as half a million dollars. Below is a chart comparing our error percentile accuracy of our most accurate model so far with Zillow's reported accuracy in Boston, MA.  

| | Our GBRT | Zillow |
| --------- | :-------: | :----: |
| Within 5% | 0.286 | 0.353 |
| Within 10% | 0.528 | 0.626 |
| Within 20% | 0.823 | 0.878 |

It's getting there. Our numbers aren't quite close enough to serve as a reliable tool yet but it's worth pointing out what a result we're getting with our limited data. Zillow's numbers have access to historical home data including historical sale prices (if a home sold for $760,000 two years ago, predicting it'll sell for $760,000 + relative area growth would be an easy but comparably accurate algorithm), meangwhile all our algorithm has is the physical features of a home. It has to play the role of an appraiser using what accounts to only the information you'd find on an real estate shop window flyer which is a significantly tougher job. The next iteration will take the best model from this iteration - gradient boosted regression trees and build upon it.


## Iteration 1

This was the tuning iteration and after letting RandomSearch run for several hours trying thousands of parameter combinations we end up with the below parameters.

```python
rf = GradientBoostingRegressor(
    n_estimators=500,
    subsample=0.8,
    learning_rate=0.09,
    min_samples_leaf=7,
    min_samples_split=9,
    max_features=10,
    max_depth=8
)
```

And these are the scores and predictions for our newly tuned GBRT. While our overall R<sup>2</sup> score has only gone up a bit, our error percentile accuracy has increased quite significantly.

```
Accuracy Across 0 Folds: 0.889946546207
Accuracy Across 5 Folds: [ 0.8579455   0.84761359  0.87830055  0.85210753  0.8764793 ]
95% Confidence Interval: 0.862 (+/- 0.025)  
          Predicted                      Sale Price          

           470,188                        475,000            
           787,193                        955,000            
           628,016                        570,000            
           491,338                        453,000            
           693,249                        840,000            
           637,664                        412,000            
           563,810                        560,000            
           425,637                        415,000            
           470,643                        439,000            
           320,209                        292,000            
           432,653                        584,000            
           812,341                        745,000            
           793,035                        690,000            
           392,469                        440,000            
           554,218                        570,000            
           553,341                        415,000            
           444,175                        385,000            
           578,212                        580,000            
           356,002                        275,000            
          1,393,317                      1,325,000           

```

| | Default GBRT | Tuned GBRT | Zillow |
| --------- | :-------: | :-----: | :----: |
| Within 5% | 0.286 | 0.313 | 0.353 |
| Within 10% | 0.528 | 0.573 | 0.626 |
| Within 20% | 0.823 | 0.854 | 0.878 |


One of the helpful side-effects of decision trees is that by examining the structure of decision trees we can infer the relative importance of features. Because our GBRT is inherently based on individual decision trees we can also use GBRTs to infer feature importance. The below graph is the relative feature importance of the top 70 most important features as inferred from the tree structure after fitting the training data.

![Graph of relative feature importance](images/figure_3.png)

Note that the above graph does not account for correlations between features and can be a little misleading. Take the correlation that exists between latitude/longitude and zip-code - homes with similar coordinates will probably be in the same zip-code; they're heavily correlated features. As a result when a decision tree is choosing a feature to split it may always choose one of the correlated features over the other resulting in the constantly chosen feature appearing to have a greater importance when in reality they both have equal importance. According to most realtors location should be the most important thing on that chart - which it may very well be if you add up all the correlated location features (lng, lat, zip, city, etc). With that said the graph is still helpful as it shows that once you get past the top ten or so the rest start having a marginal impact and can be removed without a large loss in accuracy.


## Iteration 2

Given all the work required to extract features from the realtor remarks - was it worth it? The score and sample of predictions of LARS using only the realtor remarks and no other data are below -

```
Accuracy Across 0 Folds: 0.582715416131
Accuracy Across 5 Folds: [ 0.50974483  0.56988835  0.48688742  0.59240575  0.5837315 ]
Accuracy 95% Confidence Interval: 0.549 (+/- 0.083)

          Predicted                        Actual            

           905,131                        725,000            
           461,453                        485,000            
           512,924                        394,000            
           644,302                        595,000            
           419,859                        405,000            
           743,663                        448,800            
           540,983                        533,000            
           782,918                        680,000            
           533,663                        615,000            
           588,496                        938,545            
           664,178                        630,000            
           566,246                        860,000            
           507,225                        320,000            
           419,974                        322,000            
           461,453                        485,000            
          1,061,357                       964,500            
           371,848                        341,500            
           562,445                        400,000            
          1,228,060                      1,800,000           
           375,503                        580,000            
           691,279                        530,000            
           649,725                        535,000            
           556,994                        634,500            
           324,337                        446,000            
           190,026                        330,000
```

While the accuracy isn't what we've been seeing with the other data it's still remarkably accurate considering the data it's actually using. It's able to look at a paragraph like -

> 'WELL MAINTAINED RANCH HOME IN WESTFORD!  Enter into Bright Living Room area with Hardwood Flooring. Great Opportunity to Own in Westford!  3 Bedroom, 1 Bathroom Ranch Sits on Large, Private .80 Acre Lot. This Cozy Home Features Beautifully Refinished Gleaming Hardwood Floors, Eat-In Kitchen, Working Fireplace and oversized 2 Car Detached Garage.  Desirable Cul-De-Sac/Dead End Neighborhood.'

And distinguish that as describing a $500,000 home versus a $600,000 home. While not accurate enough to stand by itself it may be accurate enough that when it's predictions are fed into our best model along with the normal data, our best model's accuracy may increase.

Beyond it's help in forming predictions, by reaching into it's internal structure tfidf also allows us to discover what it believes the most 'important' phrases to be. Note that importance here doesn't necessarily imply valuable, all it means is that the most important phrases will be rare phrases that are used often for a single home but not often for other homes. Taking the quote above as an example, of the 139 phrases present the top 40 most important phrases are -

```
Phrase                                 Importance

in westford                            0.147788853766        
and oversized car                      0.132098956072        
area with hardwood flooring            0.132098956072        
flooring great                         0.132098956072        
garage desirable                       0.132098956072        
into bright                            0.129811902345        
oversized car detached garage          0.129811902345        
own in westford                        0.129811902345        
refinished gleaming hardwood           0.129811902345        
to own in westford                     0.129811902345        
well maintained ranch home             0.129811902345        
features beautifully                   0.127830766294        
living room area                       0.127830766294        
oversized car detached                 0.127830766294        
bathroom ranch                         0.126083280451        
working fireplace and                  0.126083280451        
end neighborhood                       0.124520101098        
maintained ranch home                  0.123106033368        
refinished gleaming                    0.123106033368        
ranch home in                          0.121815090673        
ranch sits on                          0.121815090673        
beautifully refinished                 0.119528036946        
ranch sits                             0.119528036946        
room area with                         0.119528036946        
sits on large                          0.119528036946        
this cozy home                         0.119528036946        
home in westford                       0.115799415052        
area with hardwood                     0.114997247718        
westford                               0.111574244758        
80                                     0.111531225274        
cozy home                              0.111531225274        
enter into                             0.109783739431        
hardwood floors eat                    0.109783739431        
hardwood floors eat in                 0.109783739431        
on large private                       0.107734074474        
this cozy                              0.106806492348        
desirable cul                          0.106363579409        
desirable cul de                       0.106363579409        
desirable cul de sac                   0.106363579409        
well maintained ranch                  0.104327997492
```

The next iteration will see us attempt to incorporate the predictions from our realtor remarks into our best model to see if we can improve accuracy further.

## Iteration 3

One of the things I failed to mention in the corresponding methods section is that in this iteration I also ran the best GBRT model through another more intensive RandomSearch to fine-tune it's parameters. The score and predictions for the new best GBRT model that doesn't use clusters or remarks is below -

```
Accuracy: 0.896683470274
(Mean) MAPE: 0.100890029598
Accuracy Across 5 Folds: [ 0.88300328  0.88441925  0.88202692  0.86018513  0.87406707]
95% Confidence Interval: 0.877 (+/- 0.018)

        Predicted                         Actual            

          417,502                        420,000            
          450,856                        460,200            
          813,658                        791,000            
          555,995                        515,000            
          946,085                        932,500            
          592,151                        675,000            
         2,744,215                      3,808,303           
          727,037                        535,000            
          507,163                        512,000            
          278,779                        293,249            
          759,306                        861,000            
          416,052                        433,000            
          771,374                        812,500            
          637,847                        575,900            
          472,047                        455,000            
          711,582                        675,000            
          473,924                        498,000            
          748,190                        755,000            
          456,516                        440,000            
          477,551                        395,000            
          601,849                        565,000            
          988,696                       1,060,000           
         1,134,641                       975,000            
          413,623                        425,000            
          291,591                        265,000
```

| | Default GBRT | Tuned GBRT | Re-Tuned GBRT | Zillow |
| --------- | :-------: | :-----: | :------: | :----: |
| Within 5% | 0.286 | 0.313 | 0.354 | 0.353 |
| Within 10% | 0.528 | 0.573 | 0.625 | 0.626 |
| Within 20% | 0.823 | 0.854 | 0.888 | 0.878 |

For the first time so far we're actually beating Zillow in both the 5% and 20% percentiles. Lets see if we can improve on it using the pipelines. The two aforementioned forms of putting the regressors together are -

1. We predict sale price using only remarks. We predict sale price using our best GBRT model which includes all data but remarks and including clusters. We run these two columns of predictions through another regressor to make a third and final prediction using just those two predictions.

  ```
  Accuracy: 0.856986478518
  (Mean) MAPE: 0.106811866976
  (Median) MAPE: 0.0791124561404
  MSE Across 5 Folds: [ 0.86926607  0.80004628  0.77608881  0.87793983  0.88351014]
  95% Confidence Interval: 0.841 (+/- 0.087)

            Predicted                        Actual            

             940,580                        910,000            
             383,424                        256,155            
             361,510                        321,000            
             960,995                        945,000            
             604,319                        360,000            
             482,669                        495,000            
             398,181                        430,000            
             635,699                        619,900            
            1,451,480                      1,860,000           
             286,226                        225,000            
             549,987                        525,000            
             697,171                        670,000            
             353,665                        339,900            
             686,366                        725,000            
             761,115                        744,500            
             250,814                        167,000            
             821,694                       1,215,000           
             607,381                        545,000            
             532,595                        593,000            
             589,121                        600,000            
             515,685                        422,000            
             545,706                        510,000            
             518,767                        660,000            
             502,793                       1,200,000           
             409,316                        225,000
  ```

  | | Default GBRT | Tuned GBRT | Re-Tuned GBRT | Pipeline 1 | Zillow |
  | --------- | :-------: | :-----: | :------: | :----: | :----: | :----: |
  | Within 5% | 0.286 | 0.313 | 0.354 | 0.330 | 0.353 |
  | Within 10% | 0.528 | 0.573 | 0.625 | 0.601 | 0.626 |
  | Within 20% | 0.823 | 0.854 | 0.888 | 0.875 | 0.878 |

  Unfortunately this pipeline topology seems to have gone backwards. Every score is lower than our base GBRT that doesn't incorporate remarks or clustering.

2. We predict sale price using only remarks. We concatenate this predicted sale price calculated from remarks with the clusters and append them to the original data set. We then run our best GBRT model over this data set to generate a final prediction.

  ```
  Accuracy: 0.916676192559
  (Mean) MAPE: 0.0960355314487
  (Median) MAPE: 0.0712364296736
  MSE Across 5 Folds: [ 0.92454141  0.89295816  0.89372988  0.87583224  0.86605714]
  95% Confidence Interval: 0.891 (+/- 0.039)

            Predicted                        Actual            

             434,294                        408,000            
             661,798                        650,000            
             377,284                        342,000            
             432,530                        422,000            
             293,811                        348,000            
             505,317                        492,500            
             508,503                        555,000            
             322,166                        350,000            
             586,081                        586,750            
             553,451                        435,000            
             461,865                        405,000            
             794,973                        760,000            
             285,059                        267,000            
             623,925                        615,650            
             384,528                        412,500            
             406,504                        443,000            
             719,200                        867,725            
             424,610                        436,400            
             328,531                        362,000            
             562,457                        619,000            
             368,481                        290,000            
             540,498                        575,000            
             712,789                        660,000            
             630,080                        573,900            
             750,046                        707,000

  ```

  | | Default GBRT | Tuned GBRT | Re-Tuned GBRT | Pipeline 1 | Pipeline 2 | Zillow |
  | --------- | :-------: | :-----: | :------: | :----: | :----: | :----: |
  | Within 5% | 0.286 | 0.313 | 0.354 | 0.330 | 0.366 | 0.353 |
  | Within 10% | 0.528 | 0.573 | 0.625 | 0.601 | 0.654 | 0.626 |
  | Within 20% | 0.823 | 0.854 | 0.888 | 0.875 | 0.899 | 0.878 |

  This pipeline seems to have faired much better and given us our best predictions yet. It's beating Zillow in every error percentile category and it's even beating Zillow when it comes to the median absolute percent error (Zillow claims a 7.5% median error in the Boston area). For the most part the predictions are very reasonable and well within the margin of error given to a realtor or appraiser. There are however some outliers that happen to be more than $100,000 off as well discuss in the [Discussion](#discussion) section.


# Discussion

The final model in the final iteration has done what we set out to do - beat Zillow's accuracy. However it's still not perfect and systematically under predicts homes when home value starts exceeding $2,000,000 as seen in the below graph. From $0 to $2,000,000 there's a fairly good mix of predictions that are both above and under actual but as soon as we hit a threshold the vast majority of our predictions are significantly below actual. A partial explanation could be the noticeably fewer number of samples of homes with values above $2M and so the model simply doesn't have enough learning criteria to predict well.

![Graph of Actual Sale Price vs. Predicted](images/figure_4.png)

Regardless it's evident that most of my prediction error is with higher value homes and there's room to improve the models to account for that. Another fault with the existing model is the clustering algorithm itself. As it is MeanShift is only generating 26 different clusters over ~16,000 homes creating an average of 615 homes per cluster. These clusters are far too large to be of any practical use as the intended purpose is to emphasis localized clusters of roughly 1 - 10 nearby homes. While shifting the algorithm to KMeans would allow us to specify the number of clusters it'll cause a substantial performance hit because of the innate relative complexity.

# Conclusions

To quote myself from the [Introduction](#introduction) -

> "The goal isn't to beat common home valuation tools like Zillow and Redfin at their own game. Instead the goal is to get similar accuracy using a much smaller subset of data for each home..."

To this purpose we've succeeded. Instead of just matching Zillow we've beaten Zillow's estimation ability both in the Boston area (7.5%) and nationally (7.9%). This in itself is impressive if only because we're using a subset of the data that Zillow's using in their estimations. Furthermore we've shown that achieving a reliable estimate of a home's sale price given only it's physical features and a short description is possible.

|    | Our Best | Zillow |
| --- | :----: | :----: |
| (Median) MAPE | 0.071 | 0.075 |
| (Predictions) Within 5% | 0.366 | 0.353 |
| (Predictions) Within 10% | 0.654 | 0.626 |
| (Predictions) Within 20% | 0.899 | 0.878 |

If we wanted to continue increasing our accuracy there are a few key paths we could go down -

1. Unsupervised learning

  Neural networks and other forms of unsupervised learning may be more suited to the intrinsically complex problem of appraising homes.

2. Larger sample size

  I've amassed a dataset of 21,657 homes but the more data the better. Especially if planning on going down the route of unsupervised learning - a large sample size is crucial.

3. More types of data

  So far we've strictly dealt with the physical characteristics of a home as well as a brief remark about it. If we decided to also use historical data like past sale prices like Zillow I'd be surprised if the accuracy went anywhere but up. There's also a plethora of additional features we could extract like distance from town centers, proximity to public transport, noise levels, walking scores, etc. All of those would have an influence on the value of a home and wouldn't require any additional data on the home to extract.


# Acknowledgements

Thanks to Dani Fleming and Marcus Collins, both realtors in Massachusetts for allowing me MLS access for the data and providing the necessary realty background.

# References

- Edith, J., J. R. Leathwick, and T. Hastie. "A Working Guide to Boosted Regression Trees." Thesis. 2008. <i>Journal of Animal Ecology</i> 77.4 (2008): 802-13. Print.
- Li, Cheng. "A Gentle Introduction to Gradient Boosting." (n.d.): n. pag. Web. 21 Dec. 2015.
- Chen, Tianqi. "Introduction to Boosted Trees." (n.d.): n. pag. Web. 21 Dec. 2015.
- Ogutu, Joseph O., Hans-Peter Peipho, and Torben Schulz-Streeck. "A Comparison of Random Forests, Boosting and Support Vector Machines for Genomic Selection." BioMed Central. BMC Proceedings, 27 May 2011. Web. 21 Dec. 2015.
- Zola, Matteo. "Ensemble Methods: Gradient Boosted Trees." Blog Addfor. N.p., 12 Oct. 2015. Web. 21 Dec. 2015.
- "Ensemble Methods." Ensemble Methods - Scikit-learn 0.17 Documentation. Scikit-learn Developers, n.d. Web. 21 Dec. 2015.
- Paruchuri, Vik. "R vs Python: Head to Head Data Analysis." Dataquest Blog. Dataquest, 7 Oct. 2015. Web. 21 Dec. 2015.
- "Classifying Text with Bag-of-words: A Tutorial." Machine Learning Made Easy. FastML, 6 Aug. 2015. Web. 21 Dec. 2015.
- "StumbleUpon Evergreen Classification Challenge." What Did You Use? (Forum). Kaggle, StumbleUpon, 11 Jan. 2013. Web. 21 Dec. 2015.
- "What Is a Zestimate? Zillow's Home Value Forecast." Zestimate. Zillow, n.d. Web. 21 Dec. 2015.
- "The Accuracy of Real Estate Websites." Redfin. Redfin, n.d. Web. 21 Dec. 2015."
- "Sklearn.decomposition.TruncatedSVD." Scikit-learn 0.17 Documentation. Scikit-learn Developers, n.d. Web. 21 Dec. 2015.
- "Scikit-learn 0.17 Documentation." Cross-validation: Evaluating Estimator Performance. Scikit-learn Developers, n.d. Web. 21 Dec. 2015.
- "Scikit-learn 0.17 Documentation." Sklearn.ensemble.GradientBoostingRegressor. Scikit-learn Developers, n.d. Web. 21 Dec. 2015.
- "Grid Search: Searching for Estimator Parameters." Scikit-learn 0.17 Documentation. Scikit-learn Developers, n.d. Web. 21 Dec. 2015.
- "Clustering." Scikit-learn 0.17 Documentation. Scikit-learn Developers, n.d. Web. 21 Dec. 2015.
