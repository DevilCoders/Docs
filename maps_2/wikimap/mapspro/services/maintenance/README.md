# Core Nmaps Maintenance

Сервис для накатывания миграций и обновления дерева ACL-прав в ходе релизов бэкенда Народной карты.

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) <br> Евклид Никифоров (euclid@yandex-team.ru) |
| Отвественные SRE | Алексей Пономарев (ponomarev@yandex-team.ru) <br> Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | [maps/wikimap/mapspro/services/maintenance](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/maintenance) |
| Сервис в ABC | [maps-core-nmaps-maintenance](https://abc.yandex-team.ru/services/maps-core-nmaps-maintenance/)|
| Проект в CI | [maps-core-nmaps-maintenance](https://a.yandex-team.ru/projects/maps-core-nmaps-maintenance/ci/actions/launches?dir=maps/wikimap/mapspro/services/maintenance) |

## Service infrastructure

### Instances, graphics, monitorings

| Deploy unit | Nanny service | Graphics panel | Monitoring checks |
| ----------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_nmaps_maintenance_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_maintenance_stable/) | [ core-nmaps-maintenance.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-maintenance-stable-panel-main/) | [ maps_core_nmaps_maintenance_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_maintenance_stable) |
| Testing | [maps_core_nmaps_maintenance_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_maintenance_testing/) | [ core-nmaps-maintenance.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-maintenance-testing-panel-main/) | [ maps_core_nmaps_maintenance_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_maintenance_testing) |
| Unstable | [maps_core_nmaps_maintenance_unstable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_nmaps_maintenance_unstable/) | [ core-nmaps-maintenance.unstable ](https://yasm.yandex-team.ru/template/panel/maps-core-nmaps-maintenance-unstable-panel-main/) | [ maps_core_nmaps_maintenance_unstable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_nmaps_maintenance_unstable) |

[Monitorings all (tag=a_prj_maps-core-nmaps-maintenance)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-nmaps-maintenance)

### Firewall macroses

| staging | URL |
|---|---|
| Stable | [ \_MAPS_CORE_NMAPS_MAINTENANCE_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MAINTENANCE_STABLE_RTC_NETS_ ) |
| Testing | [ \_MAPS_CORE_NMAPS_MAINTENANCE_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MAINTENANCE_TESTING_RTC_NETS_ ) |
| Unstable | [ \_MAPS_CORE_NMAPS_MAINTENANCE_UNSTABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_NMAPS_MAINTENANCE_UNSTABLE_RTC_NETS_ ) |

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/wiki-maintenance/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Documentation

Про выкатывание релизов [здесь](https://docs.yandex-team.ru/nmaps/release/backend).
