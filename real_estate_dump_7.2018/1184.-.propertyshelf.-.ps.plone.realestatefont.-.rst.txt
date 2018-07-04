Real Estate icon font
=====================

.. contents:: Table of Contents


Life, the Universe, and Everything
----------------------------------

``ps.plone.realestatefont`` is an icon font of svg based icons.
It is intended to use with `Propertyshelf`_'s MLS embedding.

Mostly Harmless
---------------

.. image:: https://travis-ci.org/propertyshelf/ps.plone.realestatefont.png?branch=master
    :target: http://travis-ci.org/propertyshelf/ps.plone.realestatefont
    :alt: Travis CI status

.. image:: https://coveralls.io/repos/propertyshelf/ps.plone.realestatefont/badge.png?branch=master
    :target: https://coveralls.io/r/propertyshelf/ps.plone.realestatefont?branch=master
    :alt: Coveralls status

.. image:: https://badge.fury.io/py/ps.plone.realestatefont.png
    :target: http://badge.fury.io/py/ps.plone.realestatefont
    :alt: Fury Python

.. image:: https://badge.fury.io/gh/propertyshelf%2Fps.plone.realestatefont.png
    :target: http://badge.fury.io/gh/propertyshelf%2Fps.plone.realestatefont
    :alt: Fury Github

.. image:: https://pypip.in/d/ps.plone.realestatefont/badge.png
    :target: https://pypi.python.org/pypi/ps.plone.realestatefont/
    :alt: Downloads

.. image:: https://pypip.in/v/ps.plone.realestatefont/badge.png
    :target: https://pypi.python.org/pypi/ps.plone.realestatefont/
    :alt: Latest Version

.. image:: https://pypip.in/wheel/ps.plone.realestatefont/badge.png
    :target: https://pypi.python.org/pypi/ps.plone.realestatefont/
    :alt: Wheel Status

.. image:: https://pypip.in/egg/ps.plone.realestatefont/badge.png
    :target: https://pypi.python.org/pypi/ps.plone.realestatefont/
    :alt: Egg Status

.. image:: https://pypip.in/license/ps.plone.realestatefont/badge.png
    :target: https://pypi.python.org/pypi/ps.plone.realestatefont/
    :alt: License


Available CSS class options
---------------------------

- icon_re-airport
- icon_re-bank
- icon_re-bar
- icon_re-basketball
- icon_re-bbq
- icon_re-beach-club
- icon_re-changing-room
- icon_re-cinema
- icon_re-concierge
- icon_re-equipment-rental
- icon_re-game-room
- icon_re-garden
- icon_re-gas-station
- icon_re-golf
- icon_re-gym
- icon_re-heated-pool
- icon_re-helicopter
- icon_re-hospital
- icon_re-hotel
- icon_re-laundry
- icon_re-mall
- icon_re-medical-facility
- icon_re-minimarket
- icon_re-pool
- icon_re-property-management
- icon_re-restaurant
- icon_re-rubbish
- icon_re-security
- icon_re-soccer
- icon_re-spa
- icon_re-stable
- icon_re-storage
- icon_re-tennis
- icon_re-transportation
- icon_re-volleyball


Preview
-------

.. image:: https://raw.githubusercontent.com/propertyshelf/ps.plone.realestatefont/master/docs/_images/preview_font.png
    :alt: Real Estate Icon Font Preview


Installation
------------

To enable this package in a buildout-based installation:

#. Edit your buildout.cfg and add add the following to it::

    [buildout]
    ...
    eggs =
        ps.plone.realestatefont

#. If you are using Plone, you might want to add the ``plone`` extra::

    [buildout]
    ...
    eggs =
        ps.plone.realestatefont [plone]


After updating the configuration you need to run ''bin/buildout'', which will
take care of updating your system.

Go to the 'Site Setup' page in a Plone site and click on the 'Add-ons' link.

Check the box next to ``ps.plone.realestatefont`` and click the 'Activate' button.

The CSS classes will now prepend icons as defined in the list above.

.. note::
    You may have to empty your browser cache and save your resource registries
    in order to see the effects of the product installation.


.. _`Propertyshelf`: http://propertyshelf.com
