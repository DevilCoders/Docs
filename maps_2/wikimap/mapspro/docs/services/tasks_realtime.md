# Сервис tasks_realtime

Фоновые задачи Народной Карты

## ABC
[ABC:maps-core-nmaps-tasks-realtime](https://abc.yandex-team.ru/services/maps-core-nmaps-tasks-realtime/)

## Исходники
[maps/wikimap/mapspro/services/tasks_realtime](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime)

## Воркеры
| Название | Тип | Исходники |
|---|---|---|
|[acl_clusters_updater](tasks_realtime/acl_clusters_updater.md)|daemon|[maps/wikimap/mapspro/services/tasks_realtime/src/acl_clusters_updater](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/acl_clusters_updater)|
|[acl_permissions_synchronizer](tasks_realtime/acl_permissions_synchronizer.md)|cron|[maps/wikimap/mapspro/services/tasks_realtime/src/acl_permissions_synchronizer](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/acl_permissions_synchronizer)|
|[acl_roles_dumper](tasks_realtime/acl_roles_dumper.md)|cron|[maps/wikimap/mapspro/services/tasks_realtime/src/acl_roles_dumper](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/acl_roles_dumper)|
|[approver](tasks_realtime/approver.md)|daemon + 4 cron|[maps/wikimap/mapspro/services/tasks_realtime/src/approver](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/approver)|
|[contour_denormalizer](tasks_realtime/contour_denormalizer.md)|daemon (pubsub)|[maps/wikimap/mapspro/services/tasks_realtime/src/contour_denormalizer](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/contour_denormalizer)|
|[edits_logger](tasks_realtime/edits_logger.md)|daemon (pubsub)|[maps/wikimap/mapspro/services/tasks_realtime/src/edits_logger](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/edits_logger)|
|[export_cleaner](tasks_realtime/export_cleaner.md)|cron|[maps/wikimap/mapspro/services/tasks_realtime/src/export_cleaner](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/export_cleaner)|
|[mrc_pedestrian_regions_logger](tasks_realtime/mrc_pedestrian_regions_logger.md)|daemon (pubsub)|[maps/wikimap/mapspro/services/tasks_realtime/src/mrc_pedestrian_regions_logger](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/mrc_pedestrian_regions_logger)|
|[mrc_pedestrian_tasks_generator](tasks_realtime/mrc_pedestrian_tasks_generator.md)|daemon (pubsub)|[maps/wikimap/mapspro/services/tasks_realtime/src/mrc_pedestrian_tasks_generator](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/mrc_pedestrian_tasks_generator)|
|[outsourcer_edits_worker](tasks_realtime/outsourcer_edits_worker.md)|daemon (pubsub)|[maps/wikimap/mapspro/services/tasks_realtime/src/outsourcer_edits_worker](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/outsourcer_edits_worker)|
|[outsource_regions_worker](tasks_realtime/outsource_regions_worker.md)|daemon (pubsub)|[maps/wikimap/mapspro/services/tasks_realtime/src/outsource_regions_worker](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/outsource_regions_worker)|
|[publication_check_worker](tasks_realtime/publication_check_worker.md)|cron|[maps/wikimap/mapspro/services/tasks_realtime/src/publication_check_worker](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/publication_check_worker)|
|[release_metrics](tasks_realtime/release_metrics.md)|cron|[maps/wikimap/mapspro/services/tasks_realtime/src/release_metrics](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/release_metrics)|
|[skills_updater](tasks_realtime/skills_updater.md)|cron (disabled)|[maps/wikimap/mapspro/services/tasks_realtime/src/skills_updater](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/skills_updater)|
|[stat_outsource_regions_dump_worker](tasks_realtime/stat_outsource_regions_dump_worker.md)|cron|[maps/wikimap/mapspro/services/tasks_realtime/src/stat_outsource_regions_dump_worker](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/stat_outsource_regions_dump_worker)|
|[stat_users_dump_worker](tasks_realtime/stat_users_dump_worker.md)|cron|[maps/wikimap/mapspro/services/tasks_realtime/src/stat_users_dump_worker](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/stat_users_dump_worker)|
|[user_edits_metrics](tasks_realtime/user_edits_metrics.md)|cron|[maps/wikimap/mapspro/services/tasks_realtime/src/user_edits_metrics](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/user_edits_metrics)|
|[validation_cleaner](tasks_realtime/validation_cleaner.md)|cron|[maps/wikimap/mapspro/services/tasks_realtime/src/validation_cleaner](https://a.yandex-team.ru/arc_vcs/maps/wikimap/mapspro/services/tasks_realtime/src/validation_cleaner)|
