# Liftweb sample 2.5.1 with [sbt-plugins](https://github.com/untyped/sbt-plugins)

 * Lift 2.5.1
 * sbt-runMode (development, production)
 * sbt-js
 * sbt-less
 * modernizr
 * jquery 1.8.3
 * conditional runMode snippet
 * Twitter Bootstrap included to illustrate the use of sbt shell tasks

## Goal

Optimize build process in development and production by:

 * conditional compilation js and style files depending on mode configuration.
 * concat file or not
 * compress file or not
 * simplify debugging by separating files in development mode.
 * test production output easily
 * Add custom sbt task like bash script and link to actions

## Installation

Uses [sbt-plugins](https://github.com/untyped/sbt-plugins) plugins.


## Structure

css and less in main/css
js, coffeescript, template in main/js

These directories will be filtered and copied to resourceManaged and include in webappResources.

main js and css name : "app"

## naming convention

if filename contains (rules in build.sbt)
 * .p. == production
 * .d. == development
 * .a. == add to output directory, will be included in webAppRessources path and war package.

 (a.p.xxx, a.d.xxx, a.xxx)

### e.g.:

 * app.a.d.css => main css file in development and this file will be included to output directory.
 * app.a.p.js => main js file in production and this file will be included to output directory.
 * app-part.less => not parsed if not import in any "a" file.

## Usages

start in development:

    development:start

start in production:

    production:start

stop in development:

    development:stop

stop in production:

    production:stop

dst and pst will do a stop and a start.

compile css manually:

    xxmode:less

compile js manually:

    xxmode:js

clean output:

    xxmode:clean
    to clean only css xxmode:less::clean
    to clean only js xxmode:js::clean

### Alias

> already set in .sbtrc

    alias dst=;development:stop;development:start
    alias pst=;production:stop;production:start
    alias dsl= ;development:stop;~development:start
    alias psl= ;production:stop;~production:start
    alias dstop=development:stop
    alias dstart=development:start
    alias dc = development:compile
    alias pstop=production:stop
    alias pstart=production:start
    alias pc = production:compile
    alias dclean=development:clean
    alias pclean=production:clean
    alias djclean=development:js::clean
    alias dlclean=development:less::clean

### Recommendation
make a clean before swapping modes.

For more details on sbt-plugins, refer to [sbt-plugins Readme](https://github.com/untyped/sbt-plugins).

To go further, I recommend you mix this project with the [lift-mongo.g8 produced by Tim Nelson](https://github.com/eltimn/lift-mongo.g8).

## Authors

based on https://github.com/lift/lift_25_sbt

Thanks to [lift Team](http://www.liftweb.net/) and [sbt-plugins](https://github.com/untyped/sbt-plugins) Team.

[Alexandre Richonnier](http://www.hera.cc)
[Heirko](http://www.heirko.com)

used in [Primimo - geotagged real estate ads](http://primimo.com)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:


THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
