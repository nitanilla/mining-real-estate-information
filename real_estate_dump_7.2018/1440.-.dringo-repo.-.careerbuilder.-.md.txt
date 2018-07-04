# Careerbuilder

You can apply to be a CareerBuilder Partner at http://developer.careerbuilder.com/partner_messages/new. Once you are a partner you will receive an API token and can start using this gem.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'careerbuilder'
```

And then execute:

```
$ bundle
```

Or install it yourself as:

```
$ gem install careerbuilder
```

## Configuration

Set your API token, and any other configuration settings in a place that will run prior to your API calls.

```ruby
Careerbuilder.configure do |config|
  config.api_token = 'your-api-token-goes-here'
end
```

## Job Search

You can search for a list of jobs

```ruby
jobs = Careerbuilder::Job.search({location: 'San Jose'})
```

or a specific job

```ruby
job = Careerbuilder::Job.find('any-old-id')
```

## Job Search params

If you want to perform a job search with multiple parameters you can supply them in a hash like so:

```ruby
search_params = { location: 'San Jose', keyword: 'Database Admin' }
Careerbuilder::Job.search(search_params)
```

### Available Parameters
- `keyword` - for general search (will return jobs with matches in title, body and location (`country`, `state`, `city` and `zip`) fields)
- `title`
- `employer`
- `body`
- `country`
- `state`
- `city`
- `zip`
- `function` – see list of supported functions
- `posted_at` (`yyyy-mm-dd` format)
- `job_id`
- `location` - for search in `country`, `state`, `city` and `zip` fields

### Supported Functions
- Accounting
- Admin/Clerical
- Advertising/Public Relations
- Automotive
- Aviation
- Banking
- Biotechnology/Pharmaceutical
- Building/Facilities
- Business Opportunity
- Childcare
- Communications/Media/Writers
- Construction/Trades
- Consultant
- Customer Service
- Education
- Emergency/Fire
- Engineering
- Executive
- Government - Military
- Healthcare
- Healthcare - Allied Health
- Healthcare - Nursing
- Healthcare - Physicians
- Hospitality
- Design
- Finance
- Hourly
- HR
- Insurance
- Journalism
- Law Enforcement
- Legal
- Manufacturing/Production
- Marketing
- Non-Profit
- Oil/Energy/Power
- Real Estate
- Restaurant
- Retail
- Salon/Beauty/Fitness
- Sales
- Science
- Security
- Social Services
- Supply Chain/Logistics
- Technology
- Telecommunications
- Transportation
- Travel/Tourism
- Vet/Animal Services

## Job Details

After you have performed a search you can access the data attributes like so:

```ruby
CareerBuilder::Job.search({ location: 'San Jose' }).each do |job|
  puts "Job Details: #{job.data[:employer}} - #{job.data[:title]}"
end
```

The following data attributes are available from a job

- `title`
- `employer`
- `body`
- `posted_at`
- `url`
- `function`
- `job_id`
- `advertiser_id`,
- `location` (`country`, `state`, `city`, `zip`)
- `search_position` - job's # in response

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/careerbuilder. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
