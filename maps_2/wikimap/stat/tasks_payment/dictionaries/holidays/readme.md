Holidays
========
Calculates [holidays][] dictionaries.

Dictionaries are generated for each person in the [staff dump][]. Information
about holidays is taken from OEBS.

Note. The generated dictionary is stored on the Hahn YT cluster. The token to
connect to the cluster must be provided either by means of YT_TOKEN environment
variable or `~/.yt/token` file.


Usage
-----
Command line arguments:
* `--tvm-secret <tvm-secret>` - TVM client [secret][tvm secret].
* `--date <date>` - Date (YYYY-MM-DD) dictionary must be calculated for.
* `--env <environment>` - OEBS environment: production, testing. (default: testing)

Usage example:

    ./holidays --tvm-secret tvm_secret --date 2022-01-25 --env testing


[holidays]:   https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/holidays
[staff dump]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/staff_dump
[tvm secret]: https://abc.yandex-team.ru/services/nmaps_oebs_integration/resources/?show-resource=41376779
