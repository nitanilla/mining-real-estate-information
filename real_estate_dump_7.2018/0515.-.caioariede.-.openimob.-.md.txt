# openimob
An open-source CMS solution for Real Estate websites on top of [Wagtail](https://wagtail.io/). Right now it targets brazilian real estate needs, but the idea is to make it more comprehensive.

**pt-br:** Uma solução livre de CMS para sites imobiliários, usando o [Wagtail](https://wagtail.io/) como base.

## Requirements

* Django >= 1.7.1
* Python 3
* PostgreSQL (PostGIS)

## Installation

Clone o repository

```
mkdir <project>
cd <project>
```

```
git clone https://github.com/caioariede/openimob.git
```


### Create virtual environment -- *optional step / your rules*

```
virtualenv -p python3 .venv
source .venv/bin/activate
```

### Install dependencies

```
cd openimob
pip install -r requirements.txt
```

### Review settings and change credentials

Edit the `openimob/settings/base.py` file.

### Create database

*This steps will change depending on your environment and operating system.*

```
createuser <user> -P
createdb <dbname> -O <user>
```

```
psql -d <dbname> -c "CREATE EXTENSION postgis;"
```

```
python manage.py migrate
python manage.py createsuperuser
```

```
python manage.py loaddata listing/fixtures/categories.yaml
python manage.py loaddata listing/fixtures/amenities.yaml
```

### Run, forest!

```
python manage.py runserver 0.0.0.0:8000 --nothreading
```
