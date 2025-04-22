# Core Bizdir Sps

Система приема правок по организациям для дальнейшего их разбора контент-менеджерами.

| Staging | Url                                               |
| ------- | ------------------------------------------------- |
| Stable  | https://sps-workstation.n.yandex-team.ru/         |
| Testing | https://sps-workstation-testing.n.yandex-team.ru/ |

## General information

| What                       | Who                                                                                                                                                |
| ----                       | ---                                                                                                                                                |
| Ответственные разработчики | Александр Бобков (alexbobkov@yandex-team.ru)                                                                                                       |
| Отвественные SRE           | Александр Бобков (alexbobkov@yandex-team.ru) <br> Кантемир Бажев (kan-bazhev@yandex-team.ru)                                                       |
| Исходники                  | [maps/bizdir/sps](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps)                                                                      |
| Протоколы                  | [maps/proto/bizdir](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bizdir)                                            |
| Backoffice API             | [Backoffice API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bizdir/sps/docs/BackofficeApi.md)                     |
| Workstation API            | [Workstation API](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/proto/yandex/maps/proto/bizdir/sps/docs/WorkstationApi.md)                   |
| Схема обработки сигналов   | [Обработка сигналов](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/docs/UseCases.md)                                                  |
| Структура сервиса          | [Структура сервиса](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/docs/ServiceStructure.md)                                           |
| Сервис в ABC               | [maps-core-bizdir-sps](https://abc.yandex-team.ru/services/maps-core-bizdir-sps/)                                                                  |
| CI                         | [Nanny service maps-core-bizdir-sps build flow](https://a.yandex-team.ru/projects/maps-core-bizdir-sps/ci/actions/launches?dir=maps/bizdir/sps&id=build) |

## Service infrastructure

### MDB PostgreSQL
| Staging | Url                                                                                                                  |
| ------- | ---                                                                                                                  |
| Stable  | [cluster](https://yc.yandex-team.ru/folders/akue1pdleb5oo7k9fbrc/managed-postgresql/cluster/mdbch539qvn3kem99ql5)    |
| Testing | [cluster](https://yc.yandex-team.ru/folders/akue1pdleb5oo7k9fbrc/managed-postgresql/cluster/mdbqd859ec879n63iq1n)    |

### Nanny services

| Deploy unit | Nanny service | Graphics panel | Monitoring checks |
| ----------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_bizdir_sps_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bizdir_sps_stable/) | [ core-bizdir-sps.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-bizdir-sps-stable-panel-main/) | [ maps_core_bizdir_sps_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bizdir_sps_stable) |
| Testing | [maps_core_bizdir_sps_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_bizdir_sps_testing/) | [ core-bizdir-sps.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-bizdir-sps-testing-panel-main/) | [ maps_core_bizdir_sps_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_bizdir_sps_testing) |

[Monitorings all (tag=a_prj_maps-core-bizdir-sps)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-bizdir-sps)

### Firewall macroses

| Staging | URL                                                                                                                                                                   |
|---      |---                                                                                                                                                                    |
| Stable  | [ \_MAPS_CORE_BIZDIR_SPS_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_BIZDIR_SPS_STABLE_RTC_NETS_ )  |
| Testing | [ \_MAPS_CORE_BIZDIR_SPS_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_BIZDIR_SPS_TESTING_RTC_NETS_ ) |

### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Stable  | default | [core-bizdir-sps.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-bizdir-sps.maps.yandex.net/) | [core-bizdir-sps.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,vla,man;fqdn=core-bizdir-sps.maps.yandex.net;prj=core-bizdir-sps-maps;signal=service_total;) | [rtc_balancer_core-bizdir-sps_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bizdir-sps_maps_yandex_net_man) <br>[rtc_balancer_core-bizdir-sps_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bizdir-sps_maps_yandex_net_sas) <br>[rtc_balancer_core-bizdir-sps_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-bizdir-sps_maps_yandex_net_vla) |
| Testing | common_default | [core-bizdir-sps.common.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.testing.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-bizdir-sps.common.testing.maps.yandex.net"}) | [core-bizdir-sps.common.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.testing.maps.yandex.net;prj=common.testing.maps.yandex.net;signal=core-bizdir-sps_common_testing_maps_yandex_net;) | [rtc_balancer_common_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_sas) <br>[rtc_balancer_common_testing_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_man) <br>[rtc_balancer_common_testing_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_testing_maps_yandex_net_vla) |

### Monitorings, dashboards

| Stage   | Events panel                                               | Dashboard                                                                          |
| ------- | ------------                                               | ---------                                                                          |
| Stable  | [yasm](https://yasm.yandex-team.ru/panel/ilyamukh._Pfpinp) | [Dashboard](https://datalens.yandex-team.ru/4fu9pts24yr2x-dashbord-statistiki-sps) |
| Testing | [yasm](https://yasm.yandex-team.ru/panel/ilyamukh._Xw7_Ew) | -                                                                                  |

### CHYT clique
| Cluster | Dashboard | Alert |
| ------- | --------- | ----- |
| Hahn    | [solomon](https://solomon.yandex-team.ru/?project=yt&cluster=hahn&service=clickhouse&cookie=Aggr&dashboard=chyt_v2&l.operation_alias=maps_sps_clique)   | [alert](https://solomon.yandex-team.ru/admin/projects/maps-core-bizdir-sps/alerts/sps-clique-hahn) |
| Arnold  | [solomon](https://solomon.yandex-team.ru/?project=yt&cluster=arnold&service=clickhouse&cookie=Aggr&dashboard=chyt_v2&l.operation_alias=maps_sps_clique) | [alert](https://solomon.yandex-team.ru/admin/projects/maps-core-bizdir-sps/alerts/sps-clique-arnold) |

### Sandbox schedulers

Для обновления в СПП информации по рубрикам и признакам в Sandbox запущены
шедулеры, которые берут информацию из экспорта Справочника (компонента `rubrics_loader`).
[Код](https://a.yandex-team.ru/arc_vcs/sandbox/projects/mapsearch/UpdateSpsRubricsData) таски.

| Staging | Sandbox scheduler                                                 |
| ------- | ------------                                                      |
| Stable  | [scheduler](https://sandbox.yandex-team.ru/scheduler/697476/view) |
| Testing | [scheduler](https://sandbox.yandex-team.ru/scheduler/697475/view) |

### Precommit checks

Для проекта настроены прекоммитные проверки, которые прогоняют проверку типов с
помощью `mypy` (python3.9).

[Sandbox task](https://a.yandex-team.ru/arc_vcs/sandbox/projects/mapsearch/BizdirMypyTest).
Для сандбокс таски был собран кастомный контейнер с `python3.9` и всеми
необходимыми пакетами
([что установлено в контейнере](https://a.yandex-team.ru/arc_vcs/sandbox/projects/mapsearch/BizdirMypyTest/sandbox_lxc_image/install.sh)).

[CI task config](https://a.yandex-team.ru/arc_vcs/ci/registry/projects/maps_bizdir_sps/mypy.yaml).

## What happens when service is down

- Пользовательский фидбек не попадает на разбор в СПП
- Контент-менеджеры не имеют возможности разобрать уже созданные гипотезы

## How to fix common problems

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

## Logs
| Name                          | URL/path                                                                                                                      |
|---                            |---                                                                                                                            |
| Nginx                         | /var/log/nginx/*                                                                                                               |
| Service logs                  | /var/log/yandex/maps/bizdir-sps/*                                                                                              |
| Ecstatic                      | /var/log/yandex/maps/ecstatic-agent/*                                                                                          |
| Supervisord                   | /var/log/supervisor/*                                                                                                          |
| Syslog (unfiltered)           | /var/log/syslog                                                                                                               |
| YT                            | [YQL](https://yql.yandex-team.ru): SELECT * FROM hahn.`logs/maps-log/1d/2021-12-15` WHERE tskv_format = 'bizdir-sps' limit 1; |

## How-To

{% cut "Как обновить рубрикатор для UI?" %}
Данные о рубриках и признаках хранятся в [rubricator.ts](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/workstation/frontend/src/rubricator.ts)

Новый файл можно сгенерировать тулзой [make_frontend_rubricator](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bizdir/sps/tools/make_frontend_rubricator). После генерации файла необходимо переформатировать его с помощью [prettier](https://prettier.io/docs/en/install.html):

```npx prettier --write src/rubricator.ts```

{% endcut %}
