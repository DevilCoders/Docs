Work Schedule
=============
Calculates [work schedule][] dictionaries.

Dictionaries are generated for each person in the [staff dump][]. Information
about schedules is taken from OEBS.

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

    ./work_schedule --tvm-secret tvm_secret --date 2022-01-25 --env testing


[tvm secret]: https://abc.yandex-team.ru/services/nmaps_oebs_integration/resources/?show-resource=40066835
[staff dump]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/staff_dump
[work schedule]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/work_schedule_daily
