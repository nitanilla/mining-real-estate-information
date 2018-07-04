========
 merlyn
========

A server backend for interactive online exercises.

.. image:: https://travis-ci.org/crypto101/merlyn.png
   :target: https://travis-ci.org/crypto101/merlyn
.. image:: https://coveralls.io/repos/crypto101/merlyn/badge.png?branch=master
   :target: https://coveralls.io/r/crypto101/merlyn?branch=master

Testing and documentation
=========================

Testing is done using tox_. Install it, and run it from the command
line in the repository root. This will create a virtualenv_ for each
supported environment, install the necessary things in it, run the
tests, and build the documentation.

Speeding up builds
------------------

For a faster experience, it is recommended that you configure pip_ to
use wheel_ by default, by placing the following in your
``~/.pip/pip.conf`` or equivalent::

  [global]
  use-wheel = True

  [install]
  find-links = /tmp/wheelhouse

  [wheel]
  wheel-dir = /tmp/wheelhouse

After that, build wheels out of the requirements by running the
following command once::

  pip wheel -r requirements.txt -r requirements-docs.txt -r requirements-testing.txt

That will build wheels, which are faster to install than regular
packages. You can make installations even faster by adding ``no-index
= True`` to the ``[install]`` section; that way, installations won't
even hit PyPI, further reducing latency. Keep in mind that you will
then no longer be able to use ``pip install`` to install anything,
unless you've first made a wheel out of it.

.. _tox: https://testrun.org/tox/
.. _virtualenv: https://pypi.python.org/pypi/virtualenv/
.. _pip: http://www.pip-installer.org/en/latest/
.. _wheel: http://wheel.readthedocs.org/en/latest/

Release notes
=============

0.0.9
-----

Added per-user secrets. Once pyca/cryptography will have HKDF support,
this will turn into per-user entropy.

Also minor fixes, version upgrades.

0.0.8
-----

Now being continuously tested on Travis, with coverage monitoring
thanks to Coveralls.

Several other minor improvements:

- A useful mixin for resources that represent exercises, for helping
  them resolve and notify when an exercise is completed.
- User e-mails are indexed.
- Persisted factories are now unary callables that take a store. This
  prevents some otherwise icky global mutable state.
- New behavior for adding persisted factories: addOrUpdate; don't just
  blindly add more factories with the same identifier.

0.0.7
-----

- Added support for a ``dhparam.pem``, enabling DH-based PFS
  ciphersuites. ECDH-based PFS ciphersuites is a work in progress, see
  #6.

0.0.6
-----

- Moved requirements into setup.py for easier installs
- ``clarent`` version requirement bump

0.0.5
-----

Features:

- localhost manhole support for debugging
- Only support good ciphersuites.

0.0.4
-----

Renamed to merlyn (see "Whence the name" below).

Features:

- Drastically simplified exercise API
- Authentication API based on SSL certificate verification

0.0.3
-----

Features:

- Basic documentation for steps and exercises
- Interfaces: IStep, IRenderer, IValidator (see docs)
- A renderer based on string templating (str.format)

Upgrades:

- repoze.sphinx.autointerface -> sphinxcontrib-zopeext, which appears
  to be a shinier, more updated version of the same thing

Common things between merlyn and arthur_, such as shared AMP command
classes, were moved to clarent_.

0.0.2
-----

Features:

- Exercise and Step classes
- Step validation draft
- Step solution submission interface

0.0.1
-----

Initial public release. Nothing much to see here.

Whence the name?
================

This project was originally called merlin, because the step-by-step
oracle-like model reminded me of Merlin in the AM complexity class and
`Arthur-Merlin protocols`_. It's since been renamed to merlyn, because
the primo merlin PyPI real estate has been taken up by some kind of
weird setuptools fork.

Since Arthur is the person who performs the protocol together with
Merlin, it only made sense to name the client side project `arthur`.
Finally, clarent_, named after king Arthur's ceremonial sword, holds
common tools.

.. _arthur: https://github.com/crypto101/arthur
.. _clarent: https://github.com/crypto101/clarent
.. _`Arthur-Merlin protocols`: https://en.wikipedia.org/wiki/Merlin-Arthur_protocol
