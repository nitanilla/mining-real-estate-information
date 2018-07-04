# Tolomuco Real Estate API
## An example API to be used with the Tolomuco framework

At the core of this simple Flask app is [Faker](http://www.joke2k.net/faker/).


### Usage

The API is available at [/api/](https://fake-realtor-api.herokuapp.com/api/) and can take the following GET arguments:


GET parameter | Default        | Description
--------------|----------------|-----------------------------------
per_page      |10              | the number of results per page
page          | 0              | the page number. First page is 0.
total         | `per_page * 2` | the number of results in total
seed          | 1337405335     | the random number genorator seed.


### Deployment

This simple app is deployed to Heroku when `master` is pushed to. The
`Procfile` defines the web service which is a simple gunicorn command
with `eventlet` workers. You can find the app at
[https://fake-realtor-api.herokuapp.com/](https://fake-realtor-api.herokuapp.com/).
