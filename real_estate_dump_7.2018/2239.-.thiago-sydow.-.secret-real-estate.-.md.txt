## Secret Real Estate
[ ![Codeship Status for thiago-sydow/secret-real-estate](https://codeship.com/projects/5cdbd760-c5f3-0133-1964-4e8753dd3f97/status?branch=master)](https://codeship.com/projects/138611)
[![Code Climate](https://codeclimate.com/github/thiago-sydow/secret-real-estate/badges/gpa.svg)](https://codeclimate.com/github/thiago-sydow/secret-real-estate)
[![Test Coverage](https://codeclimate.com/github/thiago-sydow/secret-real-estate/badges/coverage.svg)](https://codeclimate.com/github/thiago-sydow/secret-real-estate/coverage)
[![Issue Count](https://codeclimate.com/github/thiago-sydow/secret-real-estate/badges/issue_count.svg)](https://codeclimate.com/github/thiago-sydow/secret-real-estate)

Simple REST API Backend with basic access authentication and role-based authorization using Pundit.

- [x] It must by API (REST, JSON)
- [x] It must be secured by basic auth
- [x] It must contain User mode - with different roles (admin, user, guest)
- [x] It must limit access to given part of API depend of User role
- [x] Admin has access to everything
- [x] User can read all, create all, but update and deleted only his records (Users can't create other users)
- [x] Guest has only read access (But an account is needed to access the API, no anonymous access)
- [x] There should be at least 2 different models except User [**Property**,**PropertyInfo**  and **Visit** added]
- [x] Those models should be in relation (1 to many) [**User** has many **Visits**], [**Property** has many **Visits**]. **Visit** uses polymorphic relationship.


## Installation
```
$ git clone git@github.com:thiago-sydow/secret-real-estate.git
$ cd secret-real-estate/
$ bundle install
$ rake db:setup
```

## Usage
```
$ rails s
```

You can see the live documentation at `http://localhost:3000/swagger`
User and password for access it can be found in `db/seeds.rb`

The application is automatically deployed to Heroku when Pull Request is merged on master branch, and CI passes.
You can also see it live on here `https://secret-real-estate.herokuapp.com/swagger`. Users are the same.

I took the challenge to test the gem Grape, who had long wanted to use to build an API. It is not perfect but I liked the result and had fun learning how to use it.

I's a demo app and I didn't extend too much on the features.

If interest you to see a more complete application made by me, please visit: https://github.com/thiago-sydow/controle-de-ponto

It's an opensource app, currently with 400+ active users. 

## Running tests
```
$ rspec -fd spec/
```

## License
MIT License.
