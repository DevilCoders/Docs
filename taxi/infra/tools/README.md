Misc scripts
============

This repository contains various scripts to aggregate stats on taxi database.
Before running scripts, you need to clone taxi/backend. It is also recommended
to source `setup_environment`:

```
. setup_environment
```
or
```
TAXI_BACKEND_ROOT=/custom/path/backend . setup_environment
```

build scripts
-------------

Scripts automate actions described on https://wiki.yandex-team.ru/taxi/backend/release
helping to build custom packages, releases and hotfixes a bit faster.

db
---

Here, scripts that update or otherwise change the database are stored.

exams
-----

Scripts for maintaining exams: update licenses, load photos.

migrations
----------

Scripts for database scheme migrations. All scripts are idempotent.

drivers
-------

Operations with drivers: search, print detailed information, resolve conflicts with licenses.

one-time
--------

This is a place for custom scripts made for one specific tasks and not intended to be reusable.
When adding such script, one must briefly describe what it's for in one-time/README.md.
This description should contain the name of the task (TAXIBACKEND-NNNN) which the script solves.

stats
-----

Statistics related scripts.

vgw
---

Voice gateways related scripts.

monitoring
----------

Scripts that show system state.
