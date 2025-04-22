Puid Map
========

Generates [`puid_map`][puid_map] table.

Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - [`users_dump`][users_dump] log date (YYYY-MM-DD)
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - not used by the tool, but is required by the RJM framework. It is recommended to set it to `daily` scale.
* `--piecework-departments <department_urls>` - comma-separated list of staff department urls to be regarded as piecework departments. Defaults to `yandex_content_data_production_nkmoder,outstaff_3676_4893`.

Optional parameters:
* `--analytics <yt-dir>` - nmaps-analytics root path for [`staff_dump`][staff_dump], also used to evaluate `--results` default value. Defaults to `//home/maps/core/nmaps/analytics`.
* `--logs <yt-dir>` - logs root path for [`users_dump`][users_dump]. Defaults to `//home/logfeller/logs`.
* `--results <yt-path>` - output path for [`puid_map`][puid_map]. Defaults to `{--analytics}/dictionaries/puid_map`.

Resources:
* Yandex logins of outsourcers as specified in [`outsourcers.yaml`][outsourcers] resource.


Usage example:
```
./bin/puid_map run --dates 2020-01-25 --proxy hahn --scale daily
```

[puid_map]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/puid_map
[outsourcers]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/stat/tasks_payment/dictionaries/users/data/outsourcers.yaml
[staff_dump]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/staff_dump
[users_dump]: https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/nmaps-users-dump-log/1d
