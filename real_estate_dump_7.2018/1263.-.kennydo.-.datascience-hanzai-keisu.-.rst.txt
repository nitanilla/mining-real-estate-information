datascience-hanzai-keisu
========================

This is our final project for CS 194-16 "Introduction to Data Science" (UC Berkeley, Spring 2014).

Our goal is to see if there is a relationship between crime rates in San Francisco and the price of real estate.

Data Files
==========
In this section, we describe how we generated each file.

``sf-neighborhoods.json``
--------------------------
First, extract the ``dbf``, ``shp``, and ``shx`` files from ``ZillowNeighborhoods-CA.zip``.
Next, run::
  
  $ ogr2ogr -f GeoJSON -where 'CITY="San Francisco"' sf-neighborhoods.json ZillowNeighborhoods-CA.shp

``sfpd_incidents_2013_with_neighborhoods.csv``
----------------------------------------------
I ran the following command to get the neighborhoods of SF::

  $ ogr2ogr -where 'CITY="San Francisco"' sfneighborhoods.shp ZillowNeighborhoods-CA.shp

Next, I ran the following to make a new CSV with the neighborhood column::

  $ python make_csv_with_neighborhood.py sfpd_incident_2013.csv sfpd_incidents_2013_with_neighborhoods.csv

Data Sources
============

* `Zillow Neighborhood Boundaries <http://www.zillow.com/howto/api/neighborhood-boundaries.htm>`_

  * More specifically, we usd the neighborhoods for the city of San Francisco.

* `SFPD Reported Incidents - 2003 to Present <https://data.sfgov.org/Public-Safety/SFPD-Reported-Incidents-2003-to-Present/dyj4-n68b>`_

  * We used the reported incidents from 2013.

* TODO: add link to page Allen used for Zillow Home Index value
