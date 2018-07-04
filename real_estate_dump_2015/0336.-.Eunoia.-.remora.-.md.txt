# Remora

Lightweight gem to discover information about San Francisco real estate. Can be adapted for anywhere in California.



## Installation

Add this line to your application's Gemfile:

    gem 'remora'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install remora

## Usage

		shark = Remora::Remora.new(email, password)
		report = shark.search_in_sf("155 14 St")
		report[:neighborhood]
			=> "Inner Mission  (09C)"
		report[:building][:year_built]
			=> "1975"

For a full list of what's in a report, check `spec/remora_spec.rb`

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
