# Real Estate App

#### This is a sample rails application demonstrating how to use [Unirest](http://unirest.io/ruby.html) and [HTTP-Cookie](https://github.com/sparklemotion/http-cookie) to make HTTP requests with authorizations and cookies, specifically for the Midwest Real Estate Data (MRED) RETS API.

### Background

Aside from the standard Rails installation, this application utilizes the following gems:

```ruby
gem 'unirest'
gem 'json'
gem 'http-cookie'
gem 'dotenv-rails', '~> 2.1', '>= 2.1.1'
```

### Installation

To use this example locally, you can clone the repository to your local computer.

You will need to run bundle to account for the added dependencies.

```sh
$ bundle
```

You will also need to add a `.env` file to the root folder of the app. In this file, you will need to supply your RETS username and password.

```ruby
USERNAME=[username]
PASSWORD=[password]
```

### Resources

* [Unirest](http://unirest.io/ruby.html) - Unirest gem documentation
* [JSON](http://flori.github.io/json/doc/index.html) - JSON gem documentation
* [HTTP-Cookie](https://github.com/sparklemotion/http-cookie) - HTTP-Cookie Github repository
* [URI](https://ruby-doc.org/stdlib-2.1.1/libdoc/uri/rdoc/URI.html) - URI Ruby Documentation
* [connectMLS: RETS Developer's Start Guide](http://www.mredllc.com/rets/documents/RETS%20Developer%20Start%20Guide1.pdf)
* [MRED RETS Resources](http://mredllc.com/products_resources/rets.asp)
* [MRED RETS API Login URL](http://connectmls-rets.mredllc.com/rets/server/login)
