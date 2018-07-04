# Ruby library for fiscal invoice verification in Republic of Slovenia (Ruby koda za davčno potrjevanje računov)

## Installation
**DISCLAIMER**: ~~This code was not  tested in production yet and I can not guarantee it's completely conformed to FURS's technical specification. Test cases described below have been tested in the FURS sandbox environment.~~ (Update: as of 30.10.2016, this gem is running in production at [RankTrackr](http://ranktrackr.com) and [Nightwatch](http://nightwatch.io)). The code is a (omitted) Ruby port of  [python-furs-fiscal](https://github.com/boris-savic/python-furs-fiscal), which is offering more info and documentation on the topic and better explanation on various parameters. See also [official documentation](http://www.datoteke.fu.gov.si/dpr/files/TehnicnaDokumentacijaVer1.6.pdf). 

Add this line to your application's Gemfile:

```ruby
gem 'furs_fiscal_verification'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install furs_fiscal_verification

## Usage

### Initialize the client

```ruby
furs = Furs.new(cert_path: "/path/to/your-certificate.p12", cert_password: "PASS", production: false)
```

*You can pass either sandbox or production certificate*

### Register an immovable business premise

```ruby
response = furs.register_immovable_business_premise(
  tax_number: 10115609, 
  premise_id: 'BP105', 
  real_estate_cadastral_number: 112, 
  real_estate_building_number: 11, 
  real_estate_building_section_number: 1, 
  street: 'Trzaska cesta', 
  house_number: '24', 
  house_number_additional: 'A', 
  community: 'Ljubljana', 
  city: 'Ljubljana', 
  postal_code: '1000', 
  validity_date: Date.today, 
  software_supplier_tax_number: 24564444, 
  foreign_software_supplier_name: 'Neki')
```

If response is OK and without errors, you should receive this response:

`#<Net::HTTPOK 200 OK readbody=true>`

In case there is data/parameters missing (or they are of wrong type - be careful about integer and string parameters), you may get this:

`#<Net::HTTPOK 200 VAT error readbody=true>`

To see the error, you need to decode the response:

```ruby
JSON.parse(Base64.urlsafe_decode64(response.body.split('.')[1]))
=> {"BusinessPremiseResponse"=>{"Header"=>{"MessageID"=>"b7b1e98f-dcae-47af-b829-3237802a2688", "DateTime"=>"2016-07-27T23:15:05"}, "Error"=>{"ErrorCode"=>"S002", "ErrorMessage"=>"Sporočilo ni v skladu s shemo JSON"}}}
```

### Invoice verification

Prepare your invoice data and calculate ZOI code:

```
zoi = furs.calculate_zoi(
        tax_number: 10115609, 
        issued_date: Date.today, 
        invoice_number: '11', 
        business_premise_id: 'BP105', 
        electronic_device_id: '0001', 
        invoice_amount: 19.15)
 
 => "51a40dcabb147d1c76d843ee98f951aa"
```

Now that we got this ZOI code, we send it together with other stuff to FURS and get back the response that contains EOR (unique invoice code):

```ruby
# find other params in the source (refunds,...)
response = furs.report_invoice(
            zoi: zoi, 
            tax_number: 10115609, 
            issued_date: Date.today,
            invoice_number: '11', 
            business_premise_id: 'BP105', 
            electronic_device_id: '0001', 
            invoice_amount: 19.15, 
            low_tax_rate_base: 35.14, 
            low_tax_rate_amount: 3.34, 
            high_tax_rate_base: 23.14, 
            high_tax_rate_amount: 5.09)
```

If everything goes OK, we can extract the EOR code like so:

```ruby
eor = JSON.parse(Base64.decode64(response.body.split('.')[1]))["InvoiceResponse"]["UniqueInvoiceID"]
 => "dedc5383-169f-4c0e-b369-d64ec8797170"
```

Now we have ZOI and EOR code. We need to print both to our invoice. We also need to print a QR code. The code that we use to generate the QR code is generated like this:

```ruby
furs.prepare_printable(invoice_number, zoi, issued_date)
=> "108519284076690038963265761078884782506111607270000000"
```

Use the latter for input to your QR rendering library.

## Development

After checking out the repo, run `bin/setup` to install dependencies. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/matixmatix/furs_fiscal_verification.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

