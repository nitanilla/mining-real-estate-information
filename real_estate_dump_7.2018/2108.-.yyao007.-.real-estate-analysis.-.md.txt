# Real Estate Analysis.
There are three projects in this repo:
### 1. [BiggerPockets](https://github.com/yyao007/real-estate-analysis/tree/master/BiggerPockets)
Crawler for [BiggerPockets](https://www.biggerpockets.com/forums) forums.
### 2. [activerain](https://github.com/yyao007/real-estate-analysis/tree/master/activerain)
Crawler for [activerain](http://activerain.com/bloghome) blogs.
### 3. [reanal](https://github.com/yyao007/real-estate-analysis/tree/master/reanal)
+ Analyze the posts from both sites using natural language processing tools (nltk and sklearn) to find the key phrase for every city, state in every month.
+ Use machine learning methods such as Naive Bayes Classifier to identify sentiment for posts from every city, state in every month.
+ Use Stanford CoreNLP library to extract location from each post. ([corenlp server issue](https://github.com/yyao007/real-estate-analysis/blob/master/reanal/README.md#corenlp-server-issue))

## Steps to run the whole project
#### 1. Crawl from BiggerPockets and activerain
This step takes about two days
```
$ cd /real-estate-analysis/BiggerPockets/
$ ./start.sh # run BiggerPockets crawler
$ cd /real-estate-analysis/activerain/
$ ./start.sh # activerain crawler can run at the same time
```
#### 2. Normalize city and state for newly added user
This step is fast
```
$ cd /real-estate-analysis/reanal/
$ python nlp.py convert -n state
$ python nlp.py convert -n city
```
#### 3. Extract location from each post
This step finishes in one day (or a few hours)
```
$ cd /real-estate-analysis/reanal/
$ python nlp.py location
```
#### 4. Extract top 50 key phrases and classify sentiment for posts from every (city, state, month)
This step takes few hours
```
$ cd /real-estate-analysis/reanal/
$ python nlp.py features
$ python nlp.py sentiment # can run at the same time with features
```

## Directory Structure
```
.
├── BiggerPockets
│   ├── BiggerPockets
│   │   ├── __init__.py
│   │   ├── items.py
│   │   ├── middlewares.py
│   │   ├── pipelines.py
│   │   ├── settings.py
│   │   └── spiders
│   │       ├── __init__.py
│   │       └── forum.py
│   ├── LICENSE.md
│   ├── README.md
│   ├── requirements.txt
│   ├── scrapy.cfg
│   └── start.sh
├── LICENSE.md
├── README.md
├── activerain
│   ├── LICENSE.md
│   ├── README.md
│   ├── activerain
│   │   ├── __init__.py
│   │   ├── items.py
│   │   ├── middlewares.py
│   │   ├── pipelines.py
│   │   ├── settings.py
│   │   └── spiders
│   │       ├── __init__.py
│   │       └── blog.py
│   ├── scrapy.cfg
│   └── start.sh
├── reanal
│   ├── README.md
│   ├── __init__.py
│   ├── classifier
│   │   ├── NBClassifier
│   │   ├── NBClassifier_movie_review
│   │   └── NBClassifier_twitter
│   ├── nlp.py
│   ├── other
│   │   └── tensorflow.sh
│   └── util
│       ├── __init__.py
│       ├── convert.py
│       ├── corenlp.py
│       ├── db.py
│       ├── features.py
│       ├── location.py
│       ├── main.py
│       └── sentiment.py
└── requirements.txt

10 directories, 41 files
```

## Install Dependencies
To install dependencies, create a [virtual environment](https://virtualenv.pypa.io/en/stable/userguide/) first. In the virtual enviroment, run
```
pip install -r requirements.txt
```

