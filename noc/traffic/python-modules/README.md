traffic-team-python-modules
===========================

Set of utility functions and variables which commonly required on load balancers
and some other TT servers. Heavily used in nocbalancer
[package](https://a.yandex-team.ru/arc/trunk/arcadia/traffic/nocbalancer).

contents
--------

Package divided into this modules:
    * constants
    * log
    * output
    * system
    * utils

__constants__ is just a set of different constants

__log__ module covers reading and writing of log files.

__output__ provides functions to generate messages for Juggler passive checks,
descriptions in Juggler parlance.

Functions in __system__ interacts with OS, executing binaries, parsing /proc files,
etc..

__utils__ contains stuff that doesn't fit elsewhere.

usage
-----

Look at function docstrings, most of this functions is pretty simple.
