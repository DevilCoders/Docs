Assessment Report
=================
Calculates [assessment report][report] for the provided dates.

The report is generated from:
- [`assessment.grade`][assessment.grade] and [`assessment.unit`][assessment.unit] tables;
- social [feedback table] (feedback tasks);
- [`social.commit_event`][social.commit_event] table and [moderation logs] (moderation tasks);
- [`social.commit_event`][social.commit_event], [`social.task_active`][social.task_active] and [`social.task_closed`][social.task_closed] tables (edit tasks);
- [tasks payment dictionaries][dicts dir] and [geodata][geodata dir];
- [assessment log][] and [Tracker YT replica][].

Usage
-----
This tool is a classical RJM command line tool with the following required parameters:
* `--dates <date>` - dates (YYYY-MM-DD), the report must be calculated for.
* `--proxy <cluster>` - cluster where calculations must be run.
* `--scale <scale>` - only `daily` scale is supported.

Usage example:

    ./assessment_report run --proxy hahn --scale daily --dates 2020-01-25 2020-01-26


Report Publishing
-----------------
By default, generated report is published on [stat-beta.yandex-team.ru][beta report]. To publish this report on [stat.yandex-team.ru][report] `--publish-production` parameter must be used.


Monitorings
-----------
This report calculation is based on DB replica on YT. The replication process could be unstable, therefore there is a monitoring for replication process (see [below](#postgresql-to-yt-replication-monitoring)).


### What to Do in Case of an Alarm?
It is better to pause Nirvana [reaction] that calculates this report if replication lag is bigger than 1 day. This report is calculated every night for the day before yesterday, so lag bigger than one day could lead to wrong calculations.


### PostgreSQL to YT Replication Monitoring
This monitoring checks replication lag between `assessment` schema and its replica on YT. Data is [transferred][transfer] by [Transfer Manager][tm]. There is a [dashboard] that contains all needed information about the replication process.

Since Transfer Manager uses [Solomon] and NMAPs uses [Juggler] the following schema is used:
1. There is a [PostgreSQL to YT Replication Delay (Assessment) alert][solomon-alert] in Solomon.
2. This alert produces raw events [`host=solomon-alert & service=hahn.//home/maps/core/nmaps/dynamic/replica/assessment`][raw-event] in Juggler by means of [channel].
3. These raw events are aggregated to a Juggler check [`host=solomon-alert & service=nmaps_dynamic_replica_assessment`][juggler-check].


[assessment log]:      https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/tasks_logs/assessment_log
[assessment.grade]:    https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/assessment/assessment_grade
[assessment.unit]:     https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/assessment/assessment_unit
[feedback table]:      https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/feedback/db/feedback_latest
[moderation logs]:     https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/tasks_logs/moderation_log
[social.commit_event]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/social/social_commit_event
[social.task_active]:  https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/social/social_task_active
[social.task_closed]:  https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/dynamic/replica/social/social_task_closed
[Tracker YT replica]:  https://yt.yandex-team.ru/hahn/navigation?path=//home/startrek/tables/prod/yandex-team/queue/maps-pw

[dicts dir]:      https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/tasks_payment/dictionaries
[geodata dir]:    https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/geo-data

[beta report]:    https://stat-beta.yandex-team.ru/Maps.Wiki/Quality/Assessment
[report]:         https://stat.yandex-team.ru/Maps.Wiki/Quality/Assessment

[channel]:        https://solomon.yandex-team.ru/admin/projects/maps-nmaps/channels/6b22854e-9ca3-4ab5-9b6b-f4a30f64703e
[dashboard]:      https://solomon.yandex-team.ru/?project=data-transfer&cluster=rtc-prod&dashboard=transfer_dashboard&l.resource_id=*dtt1umh7akj2lpeun0u3&l.source_type=pg&l.target_type=yt&l.source_id=mdb6od92oiks2maqel86&l.target_id=hahn--home-maps-nmaps-dynamic-replica-assessment&b=1h
[juggler-check]:  https://juggler.yandex-team.ru/check_details/?host=solomon-alert&service=nmaps_dynamic_replica_assessment
[juggler]:        https://juggler.yandex-team.ru
[raw-event]:      https://juggler.yandex-team.ru/raw_events/?query=host%3Dsolomon-alert%26service%3Dhahn.%2F%2Fhome%2Fmaps-nmaps%2Fdynamic%2Freplica%2Fassessment
[reaction]:       https://nirvana.yandex-team.ru/browse?selected=6866797
[solomon-alert]:  https://solomon.yandex-team.ru/admin/projects/maps-nmaps/alerts/aa4a1c8a-91ba-4537-8b51-651f7b7a2630
[solomon]:        https://solomon.yandex-team.ru
[tm]:             https://wiki.yandex-team.ru/transfer-manager/replication
[transfer]:       https://yc.yandex-team.ru/folders/foodd8k45ru3cjjo3nte/data-transfer/transfer/dtt1umh7akj2lpeun0u3
