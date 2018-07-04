# CSV to XML Converter

> This project is a CLI application for converting CSV's to XML documents. The application has been developed using [Laravel 5.4](https://laravel.com/).

I created this project to demonstrate the following skills:

1. Ability to setup a Laravel 5+ Application.
2. Ability of creating an artisan command and knowledge of it's features.
3. Knowledge of SOLID principles.
4. Ability to convert a CSV file to an XML file.
5. Ability to leverage composer packages to build robust applications.
6. Ability to setup and use the Codeception testing framework.
7. Ability to create custom validators in Laravel.

## Potential Improvements

1. Create Custom Exceptions to handle errors.
2. Improve docblocks to get ready for automatic doc generation.
3. Improve test coverage.
4. Separate validating of fields and reading.

## Setup

### Requirements

- PHP 7.0
- MySQL (Codeception requires a database connection)

### Installation

``` bash
# install dependencies
composer install
```

## Usage

``` bash
# Custom artisan command
php artisan convert-csv:to-xml  | filePath | template | outputPath

# Usage
  convert-csv:to-xml <filePath> <template> <outputPath>

# Arguments
  filePath              The path to the file you wish to convert
  template              The XML output template you wish to use, existing options are "real-estate-transaction"
  outputPath            The path to where you wish to save your XML file

# Options
  -h, --help            Display this help message
  -v, --verbose         Increase the verbosity of messages

# Example
php artisan convert-csv:to-xml /csv/real_estate_transactions_sample.csv real-estate-transaction /xml/

```

## Tests

The testing framework used in this project is callled [Codeception](http://codeception.com/). Please make sure you setup a local database before running tests. You can connect to your database my make making the required adjustments to the ".env" file located in the root of this project. To run the tests, run the following command:
``` bash

# Run all functional tests
vendor/bin/codecept run functional
```