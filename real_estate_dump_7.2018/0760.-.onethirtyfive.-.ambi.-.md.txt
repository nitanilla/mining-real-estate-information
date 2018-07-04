**Note: Ambi is still under heavy development.**

Ambi: Domain-driven Design
==========================

What is Ambi?
-------------

Ambi is a DSL, a specialized "mini-language", for domain-driven design.

Your domain (TLD .com, .org, etc.) is actually well-disguised real estate.
And you wouldn't build a racetrack next to highrise condos, right? Like any
other development, constructing a domain requires thought, because where your
data resides is important.

Think of it as "domain-driven design." Before you expose a resource for data
consumers, Ambi helps you visualize it in the broader context of your domain.

Knowledge Requirements
----------------------

Ambi assumes you have solid knowledge (or curiosity regarding) the following:

- **HTTP**: semantics, resources, request methods, request and response headers
- **Rack**: builder, middleware, requests, and responses
- **Ruby**: you're on your own with domain-specific stuff, as you should be.
Your endpoints should return a <tt>#to_a</tt> structured like a rack response.

Usage
-----

The [Cucumber](http://cukes.info) features in this project are intended to be
living documentation of the software's capabilities. At this current stage,
there is one feature: a basic usage example of the Ambi language.

Lots of work to do still.

But in a nutshell, you construct your domain as a collection of apps. Each
domain has a name, and each of the apps it contains has a name. In Rails
parlance, an app would most likely map to a collection of resources; however,
Ambi doesn't care. It's advisable to group resources you believe will
eventually be separated into their own respectable services or applications.

Middleware is defineable at each of the three scopes: domain, app, and
exposure. You can insert middleware in whichever context suits you.

Ambi is built on top of the wonderful
[rack-mount](https://github.com/josh/rack-mount).

License
-------

Ambi is available to use under the MIT license.

[![Code Climate](https://codeclimate.com/badge.png)](https://codeclimate.com/github/onethirtyfive/ambi)