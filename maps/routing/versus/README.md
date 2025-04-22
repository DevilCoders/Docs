Versus
======

Libraries and tools for evaluating [leptidea](../../libs/leptidea) routing
quality.


Requirements
------------

* YT token. [Obtaining YT token](https://wiki.yandex-team.ru/yt/userdoc/token/)
* YQL token. Follow the
  [YQL web interface docs](https://yql.yandex-team.ru/docs/yt/interfaces/web/).
* Access to `//home/maps/users` on YT Hahn. Request via
  [IDM](https://idm.yandex-team.ru/) (`YT-Hahn` system, `maps-users` role).
* Access to
  [yamaps_dev](https://yt.yandex-team.ru/hahn/navigation?path=//sys/pool_trees/yamaps/yamaps-root/yamaps_dev&navmode=attributes)
  pool on YT Hahn. Request via [IDM](https://idm.yandex-team.ru/) (`YT-Hahn`
  system, `yamaps_dev-pool` role).


Notes
-----

The following data from YT is used:
* [Travel times](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/travel_times)
  Contains time of entering and exiting various segments of road graph edges.
  Both edge geometry and persistent IDs are stored. Used to calculate
  time-dependent jams.
* [Access log](https://yt.yandex-team.ru/hahn/navigation?path=//statbox/access-log)
  Requests from `core-driving-router.maps.yandex.net` hosts are used to collect
  source and destination points for requests.
* [Road graph](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/graph)
  Used for mapping long edge IDs to short ones, and for building routes.

`yamaps_dev-pool` is used for YT operations to speed up the process. The pool's
machines already have all the necessary graph files, but as a downside, you
cannot select a specific graph version.


How to run
----------

1. Run the [prepare-data](bin/prepare-data) script. It will generate routing
   requests, time-dependent jams, and build etalon routes. Specify the region,
   date, and time you wish to use for evaluation.
2. Run the [check-routing](bin/check-routing) script. It will build leptidea
   routes, and evaluate them against the etalons. Specify the name of your
   experiment with the `-e` parameter. Region, date, and time must be the same
   as for the step 1.

After that you can make some changes to leptidea, and run step 2 again, with
different `-e` value.

Results will be stored inside `//home/maps/users/<username>/versus` node on YT.
