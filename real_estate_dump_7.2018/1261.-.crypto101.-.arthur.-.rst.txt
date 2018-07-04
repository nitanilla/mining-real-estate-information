========
 arthur
========

.. image:: https://dl.dropbox.com/u/38476311/Logos/arthur.png

This is the client for the game-shaped exercises which are part of
Crypto 101, the introductory book on cryptography by lvh_.

Here's a screenshot of the client:

.. image:: https://dl.dropboxusercontent.com/u/38476311/hacks.png

Testing and documentation
=========================

The short version: use tox_.

The long version: see the extra notes for merlyn_.

Changelog
=========

0.0.2 (WIP)
-----------

UI features:

- A workbench, a sort of desktop on which everything sits.
- A launcher, which sits on the workbench, and lets you launch tools.
- Pop up utilities: notifications, prompts, alerts...

Connection features:

- TLS over AMP support, for TOFU/POP
- Automatic re-connection

0.0.1
-----

Ad-hoc hackery.

Whence the name?
================

The server side to this is called merlyn_, because the step-by-step
oracle-like model reminded me of Merlin in the AM complexity class and
`Arthur-Merlin protocols`_. (It's not spelled the usual Merlin,
because that primo PyPI real estate was already taken up by some weird
setuptools fork.)

Since Arthur is the person who performs the protocol together with
Merlin, it only made sense to name this project `arthur`. Finally,
clarent_, named after king Arthur's ceremonial sword, holds common
tools.

.. _lvh: https://twitter.com/lvh/
.. _tox: https://testrun.org/tox/
.. _merlyn: https://github.com/crypto101/merlyn
.. _clarent: https://github.com/crypto101/clarent
.. _`Arthur-Merlin protocols`: https://en.wikipedia.org/wiki/Merlin-Arthur_protocol
