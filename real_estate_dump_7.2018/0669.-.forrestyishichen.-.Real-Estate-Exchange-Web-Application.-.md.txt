# Real Estate Exchange

Welcome to the cmpe226-team wiki!

1. [ERD](https://github.com/forrestyishichen/CMPE226/tree/master/ERD)

2. [DDL](https://github.com/forrestyishichen/CMPE226/tree/master/DDL)

## Basic Set up

https://codehandbook.org/python-web-application-flask-mysql/

python 3.6 + flask(http://docs.jinkan.org/docs/flask/) + mysql

## Learning resources

[Flask Official Doc](http://flask.pocoo.org/docs/0.12/)

flask-mysql

pyvenv (come with python 3.6)

For differences of `virtualenv`, `pyvenv`, `venv`, `pyvenv`, `pyenv-virtualenv`, etc.,
please refer to this
[stack overflow question](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe).
This is a somehow annoying problem of python versions.

YS: In my experience, many popular libraries (such as TensorFlow and gRPC) use `virtualenv`.

## Run locally

Assume at local machine you already have a recent python 3 version (3.5 or 3.6) and pip.

```bash
# or simpler: pyvenv ~/flask
python3 -m venv ~/flask

# activate the environment 
source ~/flask/bin/activate

# install flask and other packages
pip install flask
pip install flask-mysql
pip install werkzeug

# clone this repository to your local
git clone git@github.com:forrestyishichen/CMPE226.git
cd CMPE226/app
python server.py

# after running, for deactivation of environment
deactivate
```

## Setting up database

Go to `server.py`, and change the following to your own local database user.

```
app.config['MYSQL_DATABASE_USER'] = 'user'
app.config['MYSQL_DATABASE_PASSWORD'] = 'pass'
```

To import DDL, go to the ddl

```
mysql < team5_final.sql -u yourusername -p
```

