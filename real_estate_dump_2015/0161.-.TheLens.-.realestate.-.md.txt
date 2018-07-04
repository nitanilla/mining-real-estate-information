# New Orleans real estate

[http://vault.thelensnola.org/realestate](http://vault.thelensnola.org/realestate)

This app scrapes the latest property sales in New Orleans, stores the records in a database and publishes the results with a map.

[![Build Status](https://travis-ci.org/TheLens/realestate.svg?branch=master)](https://travis-ci.org/TheLens/realestate) [![Documentation Status](https://readthedocs.org/projects/realestate/badge/?version=latest)](https://readthedocs.org/projects/realestate/?badge=latest) [![Coverage Status](https://coveralls.io/repos/TheLens/realestate/badge.svg?branch=master)](https://coveralls.io/r/TheLens/realestate?branch=master)

Documentation: https://realestate.readthedocs.org/

Issues: https://github.com/TheLens/realestate/issues

Tests: https://travis-ci.org/TheLens/realestate

Testing coverage: https://coveralls.io/r/TheLens/realestate

#### Dependencies

* Python 2.7
* PostgreSQL 9.3+
* PostGIS 2.1
* Flask
* SQLAlchemy
* Virtualenvwrapper/virtualenv

#### Setup

(Not yet sure if this setup will work or not.)

`git clone https://github.com/TheLens/realestate.git`

`cd` into the `realestate` directory.

`pip install -r requirements.txt`

`createdb realestate`

`psql realestate < backups/realestate.sql`  # For now, only available to The Lens employees. Access backup SQL file on S3.

#### Daily scripts

This will scrape, build, geocode, clean and publish the previous day's sales. These are summarized in `scripts/main.sh`, which is run on a cron job every night.

`python realestate/lib/scrape.py`

`python scripts/initialize.py`

There is also a cron task to run `scripts/backups.sh`, which creates a datestamped database backup on the server and then copies the file to S3.

#### Environment variables

Create environment variables in `~/.virtualenvs/realestate/bin/postactivate` locally. Do the same at `/home/ubuntu/.virtualenvs/realestate/bin/postactivate` on the server, but first remove "export" in each line.

```bash
export SERVER_ENGINE='postgresql://myuser:mypass@localhost/realestate'

export SERVER_CONNECTION='dbname=realestate user=myuser password=mypass'

export LRD_USERNAME='MyLandRecordsDivisionUsername'

export LRD_PASSWORD='MyLandRecordsDivisionPassword'

export DASHBOARD_USERNAME='myuser'

export DASHBOARD_PASSWORD='mypass'

export REAL_ESTATE_GMAIL_USERNAME=tthoren@thelensnola.org

export REAL_ESTATE_GMAIL_PASSWORD=mypass

```
