# PicturepathAUI

[![Build Status](https://travis-ci.org/antillas21/picturepath_aui.svg?branch=master)](https://travis-ci.org/antillas21/picturepath_aui)
[![Code Climate](https://codeclimate.com/github/antillas21/picturepath_aui/badges/gpa.svg)](https://codeclimate.com/github/antillas21/picturepath_aui)

A ruby wrapper around the PicturePath AUI API. PicturePath provides an API to post virtual tours to Realtor.com and other real estate websites.

This gem provides the same functionality than the
[picturepath](http://picturepath.rubyforge.org/) gem. Only with more
flexibility and an updated codebase.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'picturepath_aui'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install picturepath_aui

## Usage

We want to keep a simple API to make requests to the PicturePath AUI API.

Here's an example on how to walk the easiest path:

```ruby
# First, configure your client connection
client = PicturepathAUI::Client.new(username: "username", password: "password")

# Next, build your request payload
payload = PicturepathAUI::Request.new({
  site: 2845, order_number: 1234, product_line: "LINK",
  street1: "742 Evergreen Terrace", street2: nil, city: "Springfield",
  state: "IL", zip_code: 62701, mls_id: 5678,
  tour_url: "http://www.realestateagent.com/tours?id=12345678"
})

# you can perform a check request (for validation or testing purposes)
response = client.check(payload)

# to actually send the tour data to Realtor.com, use the :submit method
response = client.submit(payload)

# either method will return a PicturepathAUI::Response object
```

### Requests

You don't need to instantiate a `PicturepathAUI::Request` object to perform a
`:check or :submit` request to the PicturePath AUI API, you can pass XML
straight to these methods. Example, the following are also valid requests:

```ruby
xml = File.open("path/to/xml_file.xml").read
client = PicturepathAUI::Client.new(username: "username", password: "password")
response = client.check(xml)
response = client.submit(xml)

str_xml = <<-XML
<?xml version="1.0" encoding="UTF-8"?>
<AUI_SUBMISSION VERSION="5.1">
<TOUR>
<CUSTREFNUM/>
<ORDERNUM>1234</ORDERNUM>
<PRODUCT_LINE>LINK</PRODUCT_LINE>
<ADDRESS>
<STREET1>742 Evergreen Terrace</STREET1>
<STREET2/>
<CITY>Springfield</CITY>
<STATE>IL</STATE>
<COUNTRY CODE="USA"/>
<ZIP>62701</ZIP>
</ADDRESS>
<IDENTIFIERS>
<ID1 VALUE="1234569" TYPE="MLSID"/>
<ID2 VALUE="" TYPE="MLSID"/>
</IDENTIFIERS>
<DISTRIBUTION>
<SITE>2845</SITE>
</DISTRIBUTION>
<TOUR_URL>http://www.virtualtourco.com/tour.aspx?tourid=12345</TOUR_URL>
</TOUR>
</AUI_SUBMISSION>
XML

client = PicturepathAUI::Client.new(username: "username", password: "password")
response = client.check(str_xml)
response = client.submit(str_xml)
```

However, we thought having a helper class would greatly ease building the XML
document required by PicturePath :wink:

If building your request through a `PicturepathAUI::Request` object,
take in mind that:

* `site` key can accept a single value or an Array of values.
Though PicturePath documentation clearly states that you can provide multiple
values, they only support `2845`. I don't know what's the point in doing so,
but still, they "support it", then we allow you to do so.
* The `PicturepathAUI::Request` object will assing `nil` to any keys you omit in the Hash. Example: You don't pass in a `:street2` key and value, then,
`Request.street2` will return nil, and the corresponding XML tag will render
empty (`<STREET2/>`).

### Responses

You will get a `PicturepathAUI::Response` object from a `#check` or `#submit`
action.

The Response object responds to the following methods:

* `raw`: stores the raw XML response received from the PicturePath AUI API.
* `data`: stores a parsed version of raw XML in a Hash structure.
* `order_number`: stores ORDER_NUMBER value if a Submit request was performed.
* `status`: string value for the overall response status.
* `messages`: Array of strings with all messages returned in the response.
* `success?`: true if request was successful.
* `error?`: true if request response errored out.
* `warning?`: true if request response returned warning.

### API Version

By default, the `PicturepathAUI::Request` will use the PicturePath AUI API
version 5.1, however, you can change the API version to use when you
build out a request:

```ruby
request = PicturepathAUI::Request.new({
  api_version: "5.0",
  # ...other attributes...
})
```

Of course you will need to check the documentation as to the fields required
to populate your `PicturepathAUI::Request` object for the API version you choose.

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake rspec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/antillas21/picturepath_aui. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](contributor-covenant.org) code of conduct.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

