# Core Sprav Callcenter Processes

Фоновые процессы коллцентра

## General information

| What | Who |
| ---- | --- |
| Ответственные разработчики | Анна Ждан (likynushka@yandex-team.ru) Алексей Градсков (gradksov@yandex-team.ru) Андрей Дроздовский (tagrimar@yandex-team.ru) |
| Отвественные SRE | Анна Ждан (likynushka@yandex-team.ru) Алексей Градсков (gradksov@yandex-team.ru) Андрей Дроздовский (tagrimar@yandex-team.ru) |
| Исходники | [maps/sprav/callcenter/processes](https://a.yandex-team.ru/arc/trunk/arcadia/maps/sprav/callcenter/processes) |
| Сервис в ABC | [maps-core-sprav-callcenter-processes](https://abc.yandex-team.ru/services/maps-core-sprav-callcenter-processes/)|
| Проект в CI | [maps-core-sprav-callcenter-processes](https://a.yandex-team.ru/projects/maps-core-sprav-callcenter-processes/ci/actions/launches?dir=maps/sprav/callcenter/processes) |

## Service infrastructure

### Instances, graphics, monitorings

| Deploy unit | Nanny service | Graphics panel | Monitoring checks |
| ----------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_sprav_callcenter_processes_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sprav_callcenter_processes_stable/) | [ core-sprav-callcenter-processes.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-sprav-callcenter-processes-stable-panel-main/) | [ maps_core_sprav_callcenter_processes_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sprav_callcenter_processes_stable) |
| Testing | [maps_core_sprav_callcenter_processes_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sprav_callcenter_processes_testing/) | [ core-sprav-callcenter-processes.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-sprav-callcenter-processes-testing-panel-main/) | [ maps_core_sprav_callcenter_processes_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sprav_callcenter_processes_testing) |

[Monitorings all (tag=a_prj_maps-core-sprav-callcenter-processes)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-sprav-callcenter-processes)

### Firewall macroses

| staging | URL |
|---|---|
| Stable | [ \_MAPS_CORE_SPRAV_CALLCENTER_PROCESSES_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SPRAV_CALLCENTER_PROCESSES_STABLE_RTC_NETS_ ) |
| Testing | [ \_MAPS_CORE_SPRAV_CALLCENTER_PROCESSES_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SPRAV_CALLCENTER_PROCESSES_TESTING_RTC_NETS_ ) |

## What happens when service is down

TODO: Напишите, что происходит при отказе сервиса

## Logs
| Name | URL/path |
|---|---|
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |

## Documentation

https://docs.yandex-team.ru/sprav/callcenter/processes

## Persistent Volumes

* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
* /logs - логи, сюда ставится симлинка из /var/log
