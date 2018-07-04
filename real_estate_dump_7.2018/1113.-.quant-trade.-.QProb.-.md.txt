# QProb
[![Build Status](https://travis-ci.org/xenu256/QProb.svg?branch=master)](https://travis-ci.org/xenu256/QProb)

QProb - automatic resources aggregator/ summarization platform. It is part of old concept about content auto-generation.

## Demo(s)

~~All websites have their own theme and distribute summarized content through various channels, like Twitter, Facebook, Feedburner, RSS.~~

* ~~https://qprob.com/ (quantitative trading)~~
* ~~https://stckmrktnws.com (stock market)~~
* ~~https://bsnssnws.com/ (business)~~
* ~~https://entreprnrnws.com/ (entrepreneurship)~~
* ~~https://realestenews.com/ (real estate investing)~~
* ~~https://parameterless.com/ (technology)~~
* ~~https://webdnl.com/ (insurance)~~

All Django based frontends are visible only in dev. mode, everything moved to new v3 framework using [qprob_goapi](https://github.com/xenu256/qprob_goapi) and [qprob_frontend2](https://github.com/xenu256/qprob_frontend2).

## Technologies

* [Python](https://github.com/python/cpython) 3.6+
* [Django](https://github.com/django/django) 1.11+
* [uWSGI](https://github.com/unbit/uwsgi) 2.0.15
* Nginx
* [memcached](https://github.com/memcached/memcached)
* [sentry](https://github.com/getsentry/sentry)
* MySQL
* [Let's Encrypt](https://letsencrypt.org/)

## QProb API

For better manageability, those are now separate from this project and can work on Windows.

* [qprob_pyapi](https://github.com/xenu256/qprob_pyapi)
* [qprob_goapi](https://github.com/xenu256/qprob_goapi)

## API based apps

* [qprob_quasar](https://github.com/xenu256/qprob_quasar)
* [qprob_ion](https://github.com/xenu256/qprob_ion)

## Frontends

* v1-v2 (with this repo), Django based.
* v3 (Vue.js): [qprob_frontend](https://github.com/xenu256/qprob_frontend)
* v3.1 (Nuxt.js): [qprob_frontend](https://github.com/xenu256/qprob_frontend2)

## DevOps

* [qprob_devops](https://github.com/xenu256/qprob_devops)

## QProb status & Next generation

QProb development basically stopped and goes to Q3 (QProb v. 3).

Nextgen should be with fully automated content acquisition and other improvements to probably avoid previous mistakes:

* [Q3](https://github.com/xenu256/Q3)

## "Issues"

* Amazon doesn't allow use of their reviews. This feature is experimental.
* There were some issues with Twitter believing some accounts are created automatically (it isn't).
* Better use Postgres :-D

## Why QProb?

On the name side, it comes from "quantitative probability" tautology.
I have created it to save time when gathering information or keep up to date each day.
Then quantitative turned out to be very simply applicable to any pother subject,
so now it has +6 experimental, proof of concept sites. It was also my first Django project,
which then also led to Golang and [first mobile app](https://play.google.com/store/apps/details?id=talaikis.qprob.qprob).

## History

* 2004-2008. At first it was simple shell script that created websites out from tnohing. It ran over 1000 websites on 5 servers and generated me a home.
* 2015-2016. Qprob on Wordpress, MongoDB and Python 2.7 backend.
* 2016.. This one.

## Big Things for far Future

* A.I. generated content and/or images.
and/or:
* Automatic crawling.
