Homerun
=======

Crawls real estate sites to find houses for sale and rent.

This is what I use to keep an eye on new houses appearing on all the
relevant real estate sites (for me that's only German ones). Changing
the search URL and adding new spiders for other sites is fairly
straightforward, so it might be useful for you.

Note that the spiders use web scraping, and may get out of date if no
one uses them on a regular basis.

Dependencies
------------

- Python 2.7
- BeautifulSoup 3

Fetching houses
---------------

First you'll have to configure what spiders to use, and what search
URL to use for each, in a file called _spiders.json_. This should get
you started:

    cp spiders.sample.json spiders.json

Note that the default search URLs look for houses in Bergisch
Gladbach, Germany. This might not be what you want, and you might want
to add price and size restrictions.

With _spiders.json_ in place, the following command will invoke the
configured spiders to crawl real estate sites. The houses it finds are
stored in _houses.json_:

    bin/fetch_houses

New houses have the `new` property set to `true`.

Printing houses
---------------

This prints all the houses from _houses.json_, sorted by price/rent:

    bin/print_houses
