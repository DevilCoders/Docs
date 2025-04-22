Staff Dump
==========
Generates Json lines for [`staff_dump`][staff_dump] table.

Usage
-----
Required parameters:
* `--departments DEPARTMENT [DEPARTMENT ...]` - list of departments to dump. Departments are defined by corresponding Staff URL: `https://staff.yandex-team.ru/departments/<DEPARTMENT>`.

Optional parameters:
* `--log_level <log-level>` - override level of logging to stderr. Default is `INFO`.

Usage example:
```
export STAFF_TOKEN=...
./bin/staff_dump --departments yandex_content_data_production outstaff_3676
```

[`Authorize`][oauth] in wikimap [`application`][wikimap_app] to obtain `STAFF_TOKEN`.


[staff_dump]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries/staff_dump
[oauth]: https://oauth.yandex-team.ru/authorize?response_type=token&client_id=4e1c56227137461c8001db61232660ab
[wikimap_app]: https://oauth.yandex-team.ru/client/4e1c56227137461c8001db61232660ab
