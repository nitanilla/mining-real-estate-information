<a href="https://www.twilio.com">
  <img src="https://static0.twilio.com/marketing/bundles/marketing/img/logos/wordmark-red.svg" alt="Twilio" width="250" />
</a>

# Instant Lead Alerts for Ruby on Rails

[![Build Status](https://travis-ci.org/TwilioDevEd/lead-alerts-rails.svg?branch=master)](https://travis-ci.org/TwilioDevEd/lead-alerts-rails)

This demo application shows how to implement instant lead alerts using Ruby on Rails. Notify sales reps or agents right away when a new lead comes in for a real estate listing or other high value channel.

[Read the full tutorial here](https://www.twilio.com/docs/tutorials/walkthrough/lead-alerts/ruby/rails)!

## Local development

This project is built using [Ruby on Rails](http://rubyonrails.org/) Framework.

1. First clone this repository and `cd` into it.

   ```bash
   git clone git@github.com:TwilioDevEd/lead-alerts-rails.git
   cd lead-alerts-rails
   ```

1. Install the dependencies.

   ```bash
   bundle install
   ```

1. Copy the sample configuration file and edit it to match your configuration.

   ```bash
   cp .env.example .env
   ```

   You can find your `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN` in your
   [Twilio Account Settings](https://www.twilio.com/console/account/settings).
   You will also need a `TWILIO_NUMBER`, which you may find [here](https://www.twilio.com/console/phone-numbers/incoming).

   Run:
   ```bash
   source .env
   ```
   to export the environment variables.

1. Make sure the tests succeed.

   ```bash
   bundle exec rspec
   ```

1. Start the server.

   ```bash
   bundle exec rails s
   ```

1. Check it out at [http://localhost:3000](http://localhost:3000)

That's it!

## Meta

* No warranty expressed or implied. Software is as is. Diggity.
* [MIT License](http://www.opensource.org/licenses/mit-license.html)
* Lovingly crafted by Twilio Developer Education.
