# Long Tasks

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Андрей Лизунов (anlizev@yandex-team.ru), Михаил Плоткин (miplot@yandex-team.ru), Андрей Наплавков (naplavkov@yandex-team.ru), Дмитрий Сухов (quoter@yandex-team.ru) |
| Отвественные SRE | Дмитрий Сухов (quoter@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-nmaps-mrc-lt/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_NMAPS_MRC_LT |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_mrc_lt_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_lt_stable/) | [ core-nmaps-mrc-lt.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-lt-stable-panel-main/) | [ maps_core_nmaps_mrc_lt_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_lt_stable) |
| Datatesting | [maps_core_nmaps_mrc_lt_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_mrc_lt_datatesting/) | [ core-nmaps-mrc-lt.datatesting ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-mrc-lt-datatesting-panel-main/) | [ maps_core_nmaps_mrc_lt_datatesting ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_mrc_lt_datatesting) |
[Monitorings all (tag=a_prj_maps-core-nmaps-mrc-lt)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-mrc-lt)

| Staging | User panels |
| ------- | ----------- |
| Stable  | [dbaas_postgres_metrics](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=117eed12-3358-4c5e-b713-6cbf1d57e54e;dbname=maps_mrc) |
| Testing | [dbaas_postgres_metrics](https://yasm.yandex-team.ru/template/panel/dbaas_postgres_metrics/cid=dcddf4d9-6276-4f2a-9e11-3c07cab2ccd1;dbname=maps_mrc_testing) |
| Stable  | [mds-ns-space](https://yasm.yandex-team.ru/template/panel/mds-ns-space/prj=maps_mrc/?range=604800000)


#### Postgres -> YT replication monitoring

Данный мониторинг следит за свежестью данных в YT которые туда копируются с помощью [Трансфер менеджера](https://yc.yandex-team.ru/folders/foo90tgr8rs4tpjj5m74/data-transfer/transfer/dttidmi9v6gi8p75c1h5). Информация об активности Трансфер Менеджера сохраняется в Соломоне и доступна на [дешборде](https://solomon.yandex-team.ru/?project=data-transfer&cluster=rtc-prod&dashboard=transfer_dashboard&l.resource_id=*dttidmi9v6gi8p75c1h5&l.source_type=pg&l.target_type=yt&l.source_id=117eed12-3358-4c5e-b713-6cbf1d57e54e&l.target_id=hahn--home-maps-nmaps-dynamic-replica-mrc&b=1h). В свою очередь, в картах используется Джаглер. Для объединения этих двух систем, в Соломоне настроен [алерт PostgreSQL to YT Replication Delay (MRC)](https://solomon.yandex-team.ru/admin/projects/maps-nmaps/alerts/36ba86c0-f66f-4125-b804-73402f316985). Этот алерт пробрасывается в мониторинг настроенный в Джаглере: [`host=solomon-alert, service=nmaps_dynamic_replica_mrc`](https://juggler.yandex-team.ru/check_details/?host=solomon-alert&service=nmaps_dynamic_replica_mrc&query=&last=1DAY).

## What happens when service is down
Перестанут обрабатываться снимки из "Мобильной Народной карты" и "Приватного приложения для объездов".

## Logs
| Name | URL/path |
|---|---|
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| assignment_inspector | /var/log/yandex/maps/mrc-assignment-inspector/* |
| assignment_object_feedback_tasks_emitter | /var/log/yandex/maps/mrc-assignment-object-feedback-tasks-emitter/* |
| async_ride_correction | /var/log/yandex/maps/mrc-async-ride-correction/* |
| async_takeout_data_erasure | /var/log/yandex/maps/mrc-async-takeout-data-erasure/* |
| async_takeout_uploader | /var/log/yandex/maps/mrc-async-takeout-uploader/* |
| excess_features_eraser | /var/log/yandex/maps/mrc-excess-features-eraser/* |
| export_gen | /var/log/yandex/maps/mrc-export-generator/* |
| feature_publisher | /var/log/yandex/maps/mrc-feature-publisher/* |
| feedback_stat | /var/log/yandex/maps/mrc-feedback-stat/* |
| graph_coverage_export | /var/log/yandex/maps/mrc-graph-coverage-export/* |
| import_taxi | /var/log/yandex/maps/mrc-import-taxi/* |
| privacy_guard | /var/log/yandex/maps/mrc-privacy-guard/* |
| red_card | /var/log/yandex/maps/mrc-red-card/* |
| regular_upload | /var/log/yandex/maps/mrc-regular-upload/* |
| ride_inspector | /var/log/yandex/maps/mrc-ride-inspector/* |
| signs_export_gen | /var/log/yandex/maps/mrc-signs-export-generator/* |
| tasks_gen | /var/log/yandex/maps/mrc-tasks-gen-worker/* |
| taxi_stat | /var/log/yandex/maps/mrc-taxi-stat/* |
| toloka_manager_cron_jobs | /var/log/yandex/maps/mrc-toloka-manager-cron-jobs/* |
| ugc_uploader | /var/log/yandex/maps/mrc-ugc-uploader/* |
| user_activity_stat | /var/log/yandex/maps/mrc-user-activity-stat/* |
| yt_features_exporter | /var/log/yandex/maps/mrc-yt-features-exporter/* |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Documentation

## Known clients
- "Мобильная Народная карта";
- "Приватное приложение для объездов".

## Ecstatic Datasets
| Stable | Testing |
| ------ | ------- |
| [yandex-maps-coverage5-geoid](http://ecstatic.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) | [yandex-maps-coverage5-geoid](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions) |
| [yandex-maps-geodata6](http://ecstatic.maps.yandex.net/pkg/yandex-maps-geodata6/versions) | [yandex-maps-geodata6](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-geodata6/versions) |
| [yandex-maps-graph-activator](http://ecstatic.maps.yandex.net/pkg/yandex-maps-graph-activator/versions) | [yandex-maps-graph-activator](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-graph-activator/versions) |
| [yandex-maps-graph-compact](http://ecstatic.maps.yandex.net/pkg/yandex-maps-graph-compact/versions) | [yandex-maps-graph-compact](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-graph-compact/versions) |
| [yandex-maps-graph-compact-edges-persistent-index](http://ecstatic.maps.yandex.net/pkg/yandex-maps-graph-compact-edges-persistent-index/versions) | [yandex-maps-graph-compact-edges-persistent-index](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-graph-compact-edges-persistent-index/versions) |
| [yandex-maps-graph-compact-rtree](http://ecstatic.maps.yandex.net/pkg/yandex-maps-graph-compact-rtree/versions) | [yandex-maps-graph-compact-rtree](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-graph-compact-rtree/versions) |
| [yandex-maps-pedestrian-graph-fb](http://ecstatic.maps.yandex.net/pkg/yandex-maps-pedestrian-graph-fb/versions) | [yandex-maps-pedestrian-graph-fb](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-pedestrian-graph-fb/versions) |

## SLA

## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log
* /graph - graph storage /var/spool/yandex/maps/graph

## Firewall macroses
| staging | URL |
|---|---|
| stable | [ \_MAPS_CORE_NMAPS_MRC_LT_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MRC_LT_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_NMAPS_MRC_LT_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MRC_LT_TESTING_RTC_NETS_ ) |

## Regression Stress Testing Configurations
