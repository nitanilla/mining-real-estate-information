<a href="https://www.twilio.com">
  <img src="https://static0.twilio.com/marketing/bundles/marketing/img/logos/wordmark-red.svg" alt="Twilio" width="250" />
</a>

# Instant Lead Alerts for C# and ASP.NET MVC

[![Build status](https://ci.appveyor.com/api/projects/status/7b6v4xetbn0uy6yc/branch/master?svg=true)](https://ci.appveyor.com/project/TwilioDevEd/lead-alerts-csharp/branch/master)

This demo application shows how to implement instant lead alerts using C# and ASP.NET MVC. Notify sales reps or agents right away when a new lead comes in for a real estate listing or other high value channel.

[Read the full tutorial here!](https://www.twilio.com/docs/tutorials/walkthrough/lead-alerts/csharp/mvc)

## Local Development

1. Clone this repository and `cd` into it.

   ```shell
   $ git clone git@github.com:TwilioDevEd/lead-alerts-csharp.git
   $ cd lead-alerts-csharp
   ```

1. Copy the `LeadAlerts.Web/Local.config.example` file to `LeadAlerts.Web/Local.config`, and edit it including your credentials for the Twilio API (found at https://www.twilio.com/console/account/settings). You will also need a [Twilio Number](https://www.twilio.com/console/phone-numbers/incoming).

1. Build the solution.

1. Run the application.

1. Check it out at [http://localhost:1547](http://localhost:1547)

## Meta

* No warranty expressed or implied. Software is as is. Diggity.
* [MIT License](http://www.opensource.org/licenses/mit-license.html)
* Lovingly crafted by Twilio Developer Education.
