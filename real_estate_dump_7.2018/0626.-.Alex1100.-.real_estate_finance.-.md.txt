# RealEstateFinance

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'real_estate_finance'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install real_estate_finance

## Usage

## Functions Available

- All inputs are meant to be in their specifc order listed below and all inputs are meant to be Numbers, not Strings or Floats!

- Most outputs are Floats...

<hr/>

- gross_potential_income
    <code>
        RealEstateFinance::GrossPotentialIncome.new(monthly_income).gross_potential_income
    </code>

- net_operating_income
    <code>
        RealEstateFinance::NetOperatingIncome.new(
          monthly_income,
          vacancies,
          non_payments,
          taxes,
          mortgage_interest,
          marketing,
          advertising,
          management,
          legal,
          accounting,
          utilities,
          repairs,
          maintenance,
          acquisition,
          sale_costs
        ).net_operating_income
    </code>


- gross_rental_multiplier
    <code>
        RealEstateFinance::GrossRentalMultiplier.new(
          marketValue, 
          monthly_income
        ).gross_rental_multiplier
    </code>

- estimated_property_value_from_grm
    <code>
        RealEstateFinance::EstimatedPropertyValueFromGRM.new(
          market_value, 
          monthly_income
        ).estimated_property_value_from_grm
    </code>

- gross_operating_income
    <code>
        RealEstateFinance::GrossOperatingIncome.new(
          monthly_income, 
          estimated_loss_percentage
        ).gross_operating_income
    </code>

- capitalization_rate
    <code>
        RealEstateFinance::CapitalizationRate.new(
          monthly_income,
          vacancies,
          non_payments,
          taxes,
          marketing,
          advertising,
          management,
          legal,
          accouting,
          utilities,
          repairs,
          maintenance,
          acquisition,
          sale_costs,
          sale_earned
        ).capitalization_rate
    </code>

- estimated_property_value_from_cap_rate
    <code>
        RealEstateFinance::EstimatedPropertyValueFromCapRate.new(
            monthly_income,
            vacancies,
            non_payments,
            taxes,
            mortgage_interest,
            marketing,
            advertising,
            management,
            legal,
            accounting,
            utilities,
            repairs,
            maintenance,
            acquisition,
            sale_costs,
            sale_earned
        ).estimated_property_value_from_cap_rate
    </code>


- cash_flow_before_taxes
    <code>
        RealEstateFinance::CashFlowBeforeTaxes.new(
          monthly_income,
          vacancies,
          non_payments,
          taxes,
          mortgage_interest,
          marketing,
          advertising,
          management,
          legal,
          accounting,
          utilities,
          repairs,
          maintenance,
          acquisition,
          sale_costs,
          interest_rate,
          loan_principle,
          capital_expenditures,
          capital_expenditure_loans,
          earned_interest
        ).cash_flow_before_taxes
    </code>


- cash_flow_after_taxes
    <code>
        RealEstateFinance::CashFlowAfterTaxes.new(
          monthly_income,
          vacancies,
          non_payments,
          taxes,
          mortgage_interest,
          marketing,
          advertising,
          management,
          legal,
          accounting,
          utilities,
          repairs,
          maintenance,
          acquisition,
          sale_costs,
          interest_rate,
          loan_principle,
          capital_expenditures,
          capital_expenditure_loans,
          earned_interest,
          state_income_tax,
          federal_income_tax
        ).cash_flow_after_taxes
    </code>


- break_even_ratio
    <code>
        RealEstateFinance::BreakEvenRatio.new(
          interest_rate,
          loan_principle,
          marketing,
          advertising,
          management,
          legal,
          accounting,
          utilities,
          repairs,
          maintenance,
          monthly_income, 
          estimated_loss_percentage
        ).break_even_ratio
    </code>


- return_on_equity
    <code>
        RealEstateFinance::ReturnOnEquity.new(
            monthly_income,
            vacancies,
            non_payments,
            taxes,
            mortgage_interest,
            marketing,
            advertising,
            management,
            legal,
            accounting,
            utilities,
            repairs,
            maintenance,
            acquisition,
            sale_costs,
            interest_rate,
            loan_principle,
            capital_expenditures,
            capital_expenditure_loans,
            earned_interest,
            state_income_tax,
            federal_income_tax,
            principle_invested
        ).return_on_equity
    </code>

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/real_estate_finance.


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

