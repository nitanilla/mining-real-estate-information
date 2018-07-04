# New Orleans real estate

https://vault.thelensnola.org/realestate

This app scrapes the latest property sales in New Orleans, stores the records in a database and publishes the results with a map.

[![Build Status](https://travis-ci.org/TheLens/realestate.svg?branch=master)](https://travis-ci.org/TheLens/realestate) [![Coverage Status](https://coveralls.io/repos/github/TheLens/realestate/badge.svg?branch=master)](https://coveralls.io/github/TheLens/realestate?branch=master)

- Issues: https://github.com/TheLens/realestate/issues
- Tests: https://travis-ci.org/TheLens/realestate
- Testing coverage: https://coveralls.io/r/TheLens/realestate

#### Dependencies

* Python (2.7, 3.3, 3.4 or 3.5)
* PostgreSQL 9.3+
* PostGIS 2.1
* Flask
* SQLAlchemy
* Virtualenvwrapper

#### Setup

Run the app using Python 3. Set this up when creating the virtual environment.

```bash
mkvirtualenv --python=`which python3` realestate
```

Install the dependencies.

```bash
pip install -r requirements.txt
```

Create environment variables in `~/.virtualenvs/realestate/bin/postactivate` locally. You will need to include two lines in the server's `postactivate` file so that Upstart can find and use the variables.

```bash
REAL_ESTATE_LRD_USERNAME=MyLandRecordsDivisionUsername
REAL_ESTATE_LRD_PASSWORD=MyLandRecordsDivisionPassword
REAL_ESTATE_DATABASE_USERNAME=MyDatabaseUsername
REAL_ESTATE_DATABASE_PASSWORD=MyDatabasePassword
REAL_ESTATE_GMAIL_USERNAME=MyGmailUsername
REAL_ESTATE_GMAIL_PASSWORD=MyGmailPassword

export REAL_ESTATE_LRD_USERNAME=MyLandRecordsDivisionUsername
export REAL_ESTATE_LRD_PASSWORD=MyLandRecordsDivisionPassword
export REAL_ESTATE_DATABASE_USERNAME=MyDatabaseUsername
export REAL_ESTATE_DATABASE_PASSWORD=MyDatabasePassword
export REAL_ESTATE_GMAIL_USERNAME=MyGmailUsername
export REAL_ESTATE_GMAIL_PASSWORD=MyGmailPassword
```

Deactivate the virtualenv and activate it again to access the environment variables.

```bash
deactivate
workon realestate
```

#### Daily scripts

Every day, these two commands are run to scrape and then build, geocode, clean and publish the previous day's sales. These are summarized in `scripts/main.sh`, which is run on a cron job every night.

```bash
python scripts/scrape.py
python scripts/initialize.py
```

Occasionally, due to bugs or password expiration, you will need to scrape and build beyond the previous day. You can specify the date range for both commands by using command-line arguments.

```bash
# python scripts/scrape.py <starting_date> <ending_date>
# python scripts/scrape.py YYYY-MM-DD YYYY-MM-DD

python scripts/scrape.py 2016-05-01 2016-05-05
python scripts/initialize.py 2016-05-01 2016-05-05
```

There is also a cron task to run `scripts/backups.sh`, which creates a date-stamped database backup on the server and then copies the file to S3. This runs every night.

#### Tests

The unit tests are run using `nose`.

```bash
nosetests tests
```

You can also calculate the code coverage.

```bash
nosetests tests --with-coverage
```

__Different Python versions__

The app uses `tox` for testing different Python versions. The app is compatible and tested for Python 2.7, 3.3, 3.4 and 3.5.

```bash
tox
```
