# maps-jams-rdr-hist
Отдает информацию об исторических пробках

**Table of Contents**
[TOC]

## General information

| Key | Value |
|---|---|
| Кому звонить, если ничего не понятно | Александр Любицкий (innocent@yandex-team.ru) Евгения Мордашова (morevi@yandex-team.ru) Евгений Чернов (chereug@yandex-team.ru)|
| SRE | Вадим Мазаев (vmazaev@yandex-team.ru)  |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/jams/renderer2/historic |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-jams-rdr-hist |
| CI | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_JAMS_RDR_HIST |

## Instances

| Environment   | URL                                                          |
| ------------- | ------------------------------------------------------------ |
| **Dashboard** | https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/maps-jams-rdr-hist |
| Testing       | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_hist_testing |
| Load          | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_hist_load |
| Prestable     | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_hist_prestable |
| Stable        | https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_jams_rdr_hist_stable |

## Balancers

| Environment             | URL      |
|-------------------------|----------|
| Stable                  | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-jams-rdr-hist.maps.yandex.net |
| Testing (maps communal) | https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/backends/list/maps_core_jams_rdr_hist_testing_man/show/ |

## Graphics

| Staging   | URL            |
|-----------|----------------|
| Stable    | https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-hist-stable-panel-main |
| Prestable | https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-hist-prestable-panel-main |
| Testing   | https://yasm.yandex-team.ru/template/panel/maps-core-jams-rdr-hist-testing-panel-main |

## Logs

| What | Where                |
|-------------------|---------|
| Логи сервиса      | /var/log/yandex/maps/jams_renderer/jams_renderer.log |
| Обновления карты  | /var/log/yandex/maps/jams_renderer/jams_update.log |
| nginx             | /var/log/nginx/access-tskv.log |
| ecstatic          | /var/log/yandex/maps/ecstatic-agent/ecstatic-agent.log |
| YT                | `select * from hahn.[logs/maps-log/1d/{date}] where vhost = 'core-jams-rdr-hist.maps.yandex.net'` |

## Known client
[Maps.API](https://tech.yandex.com/maps/) <br>
[Yandex Maps](http://maps.yandex.ru)

## Ecstatic datasets
* yandex-maps-jams-historic-maps
* yandex-maps-jams-design
* yandex-maps-geodata6

## Firewall macroses
| Staging | URL            |
|---------|----------------|
| Stable  | [\_MAPS_CORE_JAMS_RDR_HIST_STABLE_RTC_NETS\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_RDR_HIST_STABLE_RTC_NETS_) |
| Testing | [\_MAPS_CORE_JAMS_RDR_HIST_TESTING_RTC_NETS\_](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_JAMS_RDR_HIST_TESTING_RTC_NETS_) |

## What happens when service is down
Исторические пробки отображаются некорректно.

## How to fix common problems
Данные могут устареть из-за проблем с генерацией карт.
Смотреть sandbox scheduler'ы:
  * stable: https://sandbox.yandex-team.ru/scheduler/13929/view
  * testing: https://sandbox.yandex-team.ru/scheduler/13525/view

Сами данные могут быть кривые, смотреть лог обновления: /var/log/yandex/maps/jams_renderer/jams_update.log

Посмотреть, что с данными в ecstatic'е, там же есть ошибки switch'ей:
  * stable: http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-jams-historic-maps/versions
  * testing: http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-jams-historic-maps/versions

## Secrets
https://nanny.yandex-team.ru/ui/#/keychains/core-jams-rdr-hist.maps.yandex.net/secrets

## Monitorings

| Staging | URL            |
|---------|----------------|
| Stable  | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_hist_stable |
| Testing | https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_jams_rdr_hist_testing |

## Maps creation

**Schedulers**:
| Staging | URL |
|---------|-----|
| Stable  | https://sandbox.yandex-team.ru/scheduler/13929/view |
| Testing | https://sandbox.yandex-team.ru/scheduler/13525/view |

**Как обновить**:
Указать ревизию Аркадии и путь к пакету (maps/jams/renderer2/historic/pkg) в sandbox scheduler'ах. Конфиги, geodata, geoid, trf и прочее берутся из этой ревизии.

## SLA
Правильно обслуживаются 99.9% запросов в месяц. <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_jams_rdr_hist.py) <br>
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_jams_rdr_hist)

## Regression Stress Testing Configurations
| Type | URL |
|------|-----|
| Graphics | https://lunapark.yandex-team.ru/regress/MAPSJAMS?service=jams_renderer#jams_renderer_hist |
| CI       |                                                     |
| Разладка | https://sandbox.yandex-team.ru/scheduler/17858/view |
| Ammo     | https://sandbox.yandex-team.ru/scheduler/45129/view |
