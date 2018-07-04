# Immobilienscout24

[![Gem Version](https://badge.fury.io/rb/immobilienscout24.svg)](http://badge.fury.io/rb/immobilienscout24)
[![Build Status](https://travis-ci.org/converate-consulting-group/immobilienscout24.svg?branch=master)](https://travis-ci.org/converate-consulting-group/immobilienscout24)
[![Dependency Status](https://gemnasium.com/converate-consulting-group/immobilienscout24.svg)](https://gemnasium.com/converate-consulting-group/immobilienscout24)

A Ruby wrapper for the Immobilienscout24 REST API. This wrapper has all the important parts for the import and export of real estates from and to Immobilienscout24.

Complete API's:

* Attachment
* Contact
* Publish
* RealEstate
* User

Incomplete:

* Search
* Expose
* Geo Services
* Product Valuation Services
* Realtor
* Construction Financing Lead engine API

In the spirit of free software, everyone is encouraged to help improve this project.

## Quick start

Add this line to your application's Gemfile:

    gem 'immobilienscout24'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install immobilienscout24

API methods are available from the `Immobilienscout24.client`.

```ruby
# Provide authentication credentials
Immobilienscout24.configure do |config|
  config.consumer_key = 'your_consumer_key'
  config.consumer_secret = 'your_consumer_secret'
end

# Fetch your real estates
immoscout_client = Immobilienscout24.client(token: 'your_oauth_token', token_secret: 'your_oauth_token_secret')
immoscout_client.real_estates
```

For the oauth process you can use the excellent [omniauth-immobilienscout24][oauthgem] gem.

[oauthgem]: https://github.com/endil/omniauth-immobilienscout24


### Consuming resources

Most methods return a [Hashie::Mash][hashie] object which provides dot notation and `[]` access for fields returned in the API response.

[hashie]: https://github.com/intridea/hashie#mash

```ruby
# Fetch the real estates
real_estates = immoscout_client.real_estates

# Sorry, we haven't invented the Immobilienscout24 response...
real_estates = real_estates["realestates.realEstates"].realEstateList.realEstateElement

# Iterate over results
real_estates.each do |real_estate|
  puts real_estate.title
  # etc.
end
```

### Creating / Updating resources

The creation / modification of resources follows one simple rule: If you make JSON requests then the object that you send via the api has to respond to `to_json`. If you make XML requests then it has to respond to `to_xml`.

```ruby
# Wrapper class for our request
class ImmoscoutEstate

  def to_json
    # generates the json for
    # the real estate that you want to create / update
  end

end

immoscout_estate = ImmoscoutEstate.new

# `to_json` will be called on the immoscout_estate object
immoscout_client.create_real_estate(immoscout_estate)
```

### Configuration

For a basic configuration you just enter your `consumer_key` and `consumer_secret`.

```ruby
Immobilienscout24.configure do |config|
  config.consumer_key = 'your_consumer_key'
  config.consumer_secret = 'your_consumer_secret'
end

# If you want to use the sandbox
config.sandbox = true

# If you want to generate a log file
config.faraday_logger = [:logger, Logger.new('log/immobilienscout24.log')]

# If you want to use xml
config.request_strategy = Immobilienscout24::Api::Request::Xml
```

There are more advanced configuration options. Take a look at `Immobilienscout24::Configuration`.

### Rails integration

Take a look at the [wiki][wiki].

[wiki]: https://github.com/converate-consulting-group/immobilienscout24/wiki/Useful-notes

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## TODO

* Extend API
* Write more tests


