[![Build Status](https://travis-ci.org/kolomanschaft/updatejunkie.svg?branch=master)](https://travis-ci.org/kolomanschaft/updatejunkie)
# UpdateJunkie

UpdateJunkie is a simple, platform independent agent for polling article-based websites. It started out as an observer for the advertising-platform [willhaben.at]. But by adding *profiles* one can observe all kinds of article-based websites. The following list shows an overview of the profiles that are currently supported:

* Willhaben: willhaben.at is an advertising service in Austria
* Willhaben Immo: The real estate section of willhaben.at

At the moment the only available notification type is email. But it should be very easy to extend UpdateJunkie with other notification types.

## Features

* Poll article-based websites and send email notifications
* Specify arbitrary tags in articles (e.g. price, description, post-time, etc.)
* Specify notification trigger-criteria based on tags (e.g. description contains X, price lower than Y, etc.)
* Handle paging in websites
* Persistent store of already processed articles
* Configurable entirely through a RESTful JSON API and/or a JSON launch script
* Easily extendable for new websites by using Python-based profiles
 
## Dependencies

* Python (>=3.2)
* BeautifulSoup 4 (for most profiles)

## Documentation

For an explanation on how to [setup] UJ and extensive list of available [commands] and how to use the API, please consult the [wiki].

[willhaben.at]: http://www.willhaben.at/
[commands]: https://github.com/kolomanschaft/updatejunkie/wiki/Commands
[setup]: https://github.com/kolomanschaft/updatejunkie/wiki/Setup
[wiki]: https://github.com/kolomanschaft/updatejunkie/wiki