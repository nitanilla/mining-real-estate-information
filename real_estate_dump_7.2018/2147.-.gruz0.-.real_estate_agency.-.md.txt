# Real Estate Agency

[![Build Status](https://travis-ci.org/gruz0/real_estate_agency.svg?branch=master)](https://travis-ci.org/gruz0/real_estate_agency)
[![Maintainability](https://api.codeclimate.com/v1/badges/db0acd56daab29bab9ab/maintainability)](https://codeclimate.com/github/gruz0/real_estate_agency/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/db0acd56daab29bab9ab/test_coverage)](https://codeclimate.com/github/gruz0/real_estate_agency/test_coverage)
[![Security](https://hakiri.io/github/gruz0/real_estate_agency/master.svg)](https://hakiri.io/github/gruz0/real_estate_agency/master)

This project is a database for a real estate agency.

## Development

To run project the first one what you need is:

```bash
docker-compose up --build
```

It builds and runs Docker containers: `app` and `db`.

All of your changes in the project automatically applied to Docker
and you don't need to reload or rebuild container.

### System dependencies

* Docker
* Docker Compose
* Ruby 2.3.5 (already installed to Docker)
* Rails 5.1 (already installed to Docker)
* MariaDB 10.0 (as Docker image)

### Configuration

All configuration files stored in `config` directory in the project root path.
You don't need to change it, because these already prepared to run
in the Docker environment.

### Database creation

```bash
docker-compose exec app rake db:drop db:create db:migrate
```

### Database initialization

```bash
docker-compose exec app rake db:seed
```

### Database diagram (ERD)

The diagram (`erd.pdf`) will be created after each of use
the `rake db:migrate` command.

## Production

All commands are available from the application directory (eg. `/var/www/real_estate_agency/current`)

### Create default system administrator

After deploy application to production server you need to create default administrators. The command below will create
the administrators with emails `root@example.com` and `me@example.com` and default password `123456` for each of them.
The first one will have the role `service_admin` and the other will have `admin`.

**NOTE:** Do not forget to create a new administrator after successfully logged in to the web.

```bash
bundle exec rake app:create_admin
```

### Initialize dictionaries with default values

The command below will populate dictionaries (`EstateType`, `EstateProject`, `EstateMaterial`) with default values

```bash
bundle exec rake app:initialize
```

## Tests

### How to run the test suite in the Docker container

```bash
docker-compose exec app bundle exec rspec --fail-fast
```

### Travis CI

Application is ready to use Travis CI. Configuration file – `.travis.yml`.

## Docker

The application contains 2 Docker files: `Dockerfile`
and `Dockerfile.real_estate_agency`.

The first one uses by `docker-compose` to build development environment
(or Travis CI builds) and depends on public image called
`gruz0/real_estate_agency` (which builds from `Dockerfile.real_estate_agency`).

To build a new version of public image you should:

1. Run `make docker_build`
   (ensure that you increment version in `Makefile` if some changes happened)
1. Run `docker login` with username and password from hub.docker.com
1. Run `make docker_push` to publish container in hub.docker.com
