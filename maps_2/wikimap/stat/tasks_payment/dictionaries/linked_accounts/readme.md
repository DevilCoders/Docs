Linked Accounts
===============

Generates [`linked_accounts`][linked_accounts] table.

Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - date (YYYY-MM-DD) to use for [`users_dump`][users_dump].
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - not used by the tool, but is required by the RJM framework. It is recommended to set it to `daily` scale.

Optional parameters:
* `--analytics <yt-dir>` - analytics root path of [`staff_dump`][staff_dump]. Defaults to `//home/maps/core/nmaps/analytics`.
* `--logs <yt-dir>` - logs root path of [`users_dump`][users_dump]. Defaults to `//home/logfeller/logs`.
* `--results <yt-path>` - output path for [`linked_accounts`][linked_accounts]. Defaults to `{--analytics}/dictionaries/linked_accounts`.


Usage example:

    ./bin/linked_accounts run --dates 2020-01-25 --proxy hahn --scale daily


[users_dump]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-users-dump-log/1d
[staff_dump]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/staff_dump
[linked_accounts]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/linked_accounts
