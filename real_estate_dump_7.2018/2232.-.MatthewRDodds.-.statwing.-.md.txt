# Statwing

[![Build Status](https://travis-ci.org/MatthewRDodds/statwing.svg?branch=master)](https://travis-ci.org/MatthewRDodds/statwing)

Ruby wrapper for the Statwing Api. This is accomplished using the [HER](https://github.com/remiprev/her) Object Relational Mapper.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'statwing'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install statwing

## Configuration

```ruby
Statwing.configure do |config|
  config.api_key = 'your_api_key'
end
```

## Usage

Creating a User and associating a new dataset:

```ruby
@user = Statwing::User.create(partner_user_id: 'identifier')
=> #<Statwing::User(users/usr_e9gAmn3WuEeDKjDwELRisB2lNYvAJMZa) partner_user_identity="identifier" id="usr_e9gAmn3WuEeDKjDwELRisB2lNYvAJMZa">

@dataset = Statwing::Dataset.create(name: "real-estate-transactions-sample.csv",fileurl: 'https://gist.githubusercontent.com/MatthewRDodds/5bf959ec16b67fd7c421/raw/52089a06e2fc9f8b74b85f49922f792610f3b6ae/real-estate-transactions-sample.csv', users: {action: 'add', data: [{ object: 'user_id', data: "usr_e9gAmn3WuEeDKjDwELRisB2lNYvAJMZa" }]})
=> #<Statwing::Dataset:0x3fff3d1023c8>

@user.datasets
=> [#<Statwing::Dataset:0x3fff3d5fe0d4>]

@dataset.attributes
=> {"name"=>"real-estate-transactions-sample.csv",
"filesize"=>113183,
"state"=>"processed",
"shared"=>"restricted",
"created_at"=>"2015-04-08T15:07:11Z",
"parse_settings"=>{"parser"=>"csv"},
"url_base"=>
"https://export.statwing.com/p0/datasets/dat_ufz8Ycgo0NiWSjICDYNCfzszXgqUeRrQ",
"users"=>nil}

@user.datasets.first.id
=> "dat_ufz8Ycgo0NiWSjICDYNCfzszXgqUeRrQ"

Statwing::Dataset.find('dat_ufz8Ycgo0NiWSjICDYNCfzszXgqUeRrQ').users
=> [{"id"=>"usr_e9gAmn3WuEeDKjDwELRisB2lNYvAJMZa",
  "partner_user_id"=>"identifier",
  "url"=>
   "https://export.statwing.com/p0/datasets/dat_ufz8Ycgo0NiWSjICDYNCfzszXgqUeRrQ/users/usr_e9gAmn3WuEeDKjDwELRisB2lNYvAJMZa"}]
```

## Contributing

1. Fork it ( https://github.com/MatthewRDodds/statwing/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
