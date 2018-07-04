# meetup-api-python
A very simple way to get data from the meetup api and convert to CSV format.

All you have to do is 1) get a api key from meetup (https://secure.meetup.com/meetup_api/key/) and modify the https://github.com/GDG-NewYork/meetup-api-python/blob/master/getmetrics.sh file. 2) if you would like to change the meetup groups that are queried, you can modify https://github.com/GDG-NewYork/meetup-api-python/blob/master/runall.sh.

Optionally, you can load into Google BigQuery and use a visualization tools such as redash.io (requires a Google Account and a BigQuery project).   For examples of this, see https://bigquery.cloud.google.com/table/personal-real-estate:gdg.meetup and http://demo.redash.io/queries/156/source#199 (requires Google Account and BigQuery project)

![image1](https://raw.githubusercontent.com/GDG-NewYork/meetup-api-python/master/images/redash_charts_2015-03-02T05_00_22.903.png "GDG Meetup RSVP Chart over time")


