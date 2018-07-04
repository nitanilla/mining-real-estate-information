# IsYourStartupDying?

### Classifier to answer the question:
Is it dying or nah?

Uses ML neighbor classifier algorithm to let budding entrepreneurs if their startup is successful or not, just enter your company details in, sit back, cross your fingers and read your result which was calculated based on pre-existing database of over 73,000 startups.

<p align="center">
<img src="http://33.media.tumblr.com/b5a4e7d76d422c02bd4065ef63fc5e3a/tumblr_inline_nqv4l5LKid1tn8yin_500.gif">
</p>

##### Current accuracy

98.941% using k=9.

#### Usage
###### To test:

```$ python classify-startup.py test {k_value}```

###### To classify your company:

```$ python classify-startup.py name status market country city funding_value funding_rounds first_round_date last_round_date {k_value}```

_Note:_ Multi word inputs must be surrounded by `''`

* name: Company name (it doesnt relly matter what this is)
* Status: `operating`, `aquired`, `ipo` or `closed`
* market: i.e `Tourism`, `'Real Estate'`, `'Music Services'`
* country: i.e `USA`, `Canada`, `'United Kingdom'`
* city: i.e `'San Franciso'`, `London`
* funding value: Total value to date i.e `2000000`
* funding rounds: i.e `3`
* first/last round date: Date of first and last funding, `YYYY-MM-DD`

ex: `$ python classify_startup.py Generic operating 'Real Estate' USA 'San Francisco' 2000 1 2016-01-01 2016-01-01`
