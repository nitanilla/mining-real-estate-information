[![Build Status](https://api.travis-ci.org/pmarreck/mpnetwork.svg?branch=master)](https://travis-ci.org/pmarreck/mpnetwork/)

## MPNetwork

[A little real-estate listing site](https://www.mpwrealestateboard.network) built on [Elixir](https://elixir-lang.org) 1.6+, [Phoenix](http://phoenixframework.org) 1.3+ and [Postgresql](https://www.postgresql.org) 9+. The production site is hosted on [Gigalixir](https://www.gigalixir.com/).

## Features

1) All views work on mobile (responsive design)
2) Search is quite full-featured (built on top of Postgres but adds a bunch of features)
3) First Phoenix project in production use (yeah!)
4) Dual concurrent test suite deployment build tests both client-side JS as well as server-side Elixir thanks to new Travis-CI "build stages" feature
5) Images are cached via ETS in both scaled and original forms and stored in the DB
6) "Devops Zero" achieved thanks to travis-ci and gigalixir
7) Brunch used for asset packaging; at the time of this writing, things are moving to Webpack (future update perhaps)
8) Will hopefully serve as a reference project for others new to Elixir/Phoenix dev

## License

"MPNetwork" is copyright (c) 2018 Peter Marreck and MECHA LLC.
All rights reserved.

Source code is licensed under the EUPL.

Staging/demo site is hosted [here](https://staging.mpwrealestateboard.network/); use login "demo@demo.com" and password "demo".

Check [NOTICE](NOTICE) and [LICENSE](LICENSE) files for more
information.
