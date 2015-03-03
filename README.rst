Readinglist
===========

Reading list is a service that aims to synchronize a list of articles URLs
between a set of devices owned by a same account.

|travis| |readthedocs|

.. |travis| image:: https://travis-ci.org/mozilla-services/readinglist.svg?branch=master
    :target: https://travis-ci.org/mozilla-services/readinglist

.. |readthedocs| image:: https://readthedocs.org/projects/readinglist/badge/?version=latest
    :target: http://readinglist.readthedocs.org/en/latest/
    :alt: Documentation Status

API
===

* `API Design proposal
  <https://github.com/mozilla-services/readinglist/wiki/API-Design-proposal>`_
* `Online documentation <http://readinglist.readthedocs.org/en/latest/>`_


Run locally
===========

By default, readinglist persists its records inside a `PostgreSQL
<http://www.postgresql.org//>`_  database, so it has to be installed first (see the
"Install PostgreSQL" section below for more on this).

Once Redis is installed:

::

    make serve


Configuration can be changed to persist everything in memory (not
recommended). To do that, `conf/readinglist.ini` file should have the
following config::

    readinglist.storage_backend = readinglist.storage.memory



Install PostgreSQL
==================

Linux
-----

On debian / ubuntu based systems::

    apt-get install postgresql


or::

    yum install postgresql

OS X
----

Assuming `brew <http://brew.sh/>`_ is installed, Redis installation becomes:

::

    brew install postgresql


Install libffi
==============

Linux
-----

On debian / ubuntu based systems::

    apt-get install libffi-dev


OS X
----

Assuming `brew <http://brew.sh/>`_ is installed, libffi installation becomes:

::

    brew install libffi pkg-config



Run tests
=========

::

    make tests
