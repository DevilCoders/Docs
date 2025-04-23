# Core Sat

Сервис отвечает за отображение растрового слоя спутниковых снимков.

## General information
| What | Who |
| ---- | --- |
| Ответственные разработчики | Дмитрий Сухов (quoter@yandex-team.ru) Николай Федоров (unril@yandex-team.ru)|
| Отвественные SRE | Борис Чикунов (chikunov@yandex-team.ru) |
| Исходники | https://a.yandex-team.ru/arc/trunk/arcadia/maps/factory/satproxy |
| Сервис в ABC | https://abc.yandex-team.ru/services/maps-core-sat/ |
| CI (TestEnv) - Покоммитный | https://testenv.yandex-team.ru/?screen=job_history&database=maps_tests&job_name=BUILD_DOCKER_MAPS_CORE_SAT |


## Service infrastructure

[Development/Testing/Production environments WIKI](https://wiki.yandex-team.ru/maps/dev/core/environment/)

Satproxy binary release path:
```
Testing -> Prestable -> Stable
```

Ecstatic datasets release path:
```
             Testing branch,          Stable branch
Testing env: Datatestingvalidation -> Datatesting
Stable env:  Datavalidation        -> Stable/Prestable/Testing
```

### Instances, graphics, monitoring

| Staging | Nanny service | Graphics panel | Monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Datatesting | [maps_core_sat_datatesting](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sat_datatesting/) | [ core-sat.datatesting ](https://yasm.yandex-team.ru/template/panel/maps-core-sat-datatesting-panel-main/) | [ maps_core_sat_datatesting ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sat_datatesting) |
| Datatestingvalidation | [maps_core_sat_datatestingvalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sat_datatestingvalidation/) | [ core-sat.datatestingvalidation ](https://yasm.yandex-team.ru/template/panel/maps-core-sat-datatestingvalidation-panel-main/) | [ maps_core_sat_datatestingvalidation ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sat_datatestingvalidation) |
| Datavalidation | [maps_core_sat_datavalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sat_datavalidation/) | [ core-sat.datavalidation ](https://yasm.yandex-team.ru/template/panel/maps-core-sat-datavalidation-panel-main/) | [ maps_core_sat_datavalidation ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sat_datavalidation) |
| Load | [maps_core_sat_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sat_load/) | [ core-sat.load ](https://yasm.yandex-team.ru/template/panel/maps-core-sat-load-panel-main/) | [ maps_core_sat_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sat_load) |
| Prestable | [maps_core_sat_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sat_prestable/) | [ core-sat.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-sat-prestable-panel-main/) | [ maps_core_sat_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sat_prestable) |
| Stable | [maps_core_sat_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sat_stable/) | [ core-sat.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-sat-stable-panel-main/) | [ maps_core_sat_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sat_stable) |
| Testing | [maps_core_sat_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_sat_testing/) | [ core-sat.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-sat-testing-panel-main/) | [ maps_core_sat_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_sat_testing) |

[Monitorings all (tag=a_prj_maps-core-sat)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-sat)


[s3mds panel](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat;owner=1971)


### Balancers

Балансер имеет нестандартные настройки

```
modules:
    - cgi_hasher:
        parameters:
          - 'x'
          - 'y'
          - 'z'
        randomize_empty_match: true
    - balancer2:
        attempts: !f count_backends()
        rendezvous_hashing:
          request: 'GET /ping HTTP/1.1\nHost: sat.tiles.maps.yandex.net\r\n\r\n'
          delay: 1s
        unique_policy: {}
```

Модули `cgi_hasher`, `rendezvous_hashing` применяются для распределения запросов по бекендам в соответствии со значением хеша от параметров `x, y, z`, это позволяет существенно увеличить кеш-хит на бекендах.


### Balancers

| Staging | Name | AWACS Balancer | Balancer Panel | Balancer Nanny services |
| ------- | ---- | -------------- | -------------- | ----------------------- |
| Datatesting | default | [core-sat.datatesting.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-sat.datatesting.maps.yandex.net/) | [core-sat.datatesting.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=man;fqdn=core-sat.datatesting.maps.yandex.net;prj=core-sat-datatesting-maps;signal=service_total;) | [rtc_balancer_core-sat_datatesting_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sat_datatesting_maps_yandex_net_man) |
| Datatestingvalidation | common_default | [core-sat.common.datatestingvalidation.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datatestingvalidation.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-sat.common.datatestingvalidation.maps.yandex.net"}) | [core-sat.common.datatestingvalidation.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.datatestingvalidation.maps.yandex.net;prj=common.datatestingvalidation.maps.yandex.net;signal=core-sat_common_datatestingvalidation_maps_yandex_net;) | [rtc_balancer_common_datatestingvalidation_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatestingvalidation_maps_yandex_net_sas) <br>[rtc_balancer_common_datatestingvalidation_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatestingvalidation_maps_yandex_net_man) <br>[rtc_balancer_common_datatestingvalidation_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datatestingvalidation_maps_yandex_net_vla) |
| Datavalidation | common_default | [core-sat.common.datavalidation.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/common.datavalidation.maps.yandex.net/upstreams/list?filter={"idRegexp":"core-sat.common.datavalidation.maps.yandex.net"}) | [core-sat.common.datavalidation.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,man,vla;fqdn=common.datavalidation.maps.yandex.net;prj=common.datavalidation.maps.yandex.net;signal=core-sat_common_datavalidation_maps_yandex_net;) | [rtc_balancer_common_datavalidation_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datavalidation_maps_yandex_net_sas) <br>[rtc_balancer_common_datavalidation_maps_yandex_net_man](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datavalidation_maps_yandex_net_man) <br>[rtc_balancer_common_datavalidation_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_common_datavalidation_maps_yandex_net_vla) |
| Stable | default | [core-sat.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-sat.maps.yandex.net/) | [core-sat.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,vla;fqdn=core-sat.maps.yandex.net;prj=core-sat-maps;signal=service_total;) | [rtc_balancer_core-sat_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sat_maps_yandex_net_sas) <br>[rtc_balancer_core-sat_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sat_maps_yandex_net_vla) |
| Stable | internal | [core-sat-internal.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-sat-internal.maps.yandex.net/) | [core-sat-internal.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas,vla;fqdn=core-sat-internal.maps.yandex.net;prj=core-sat-internal-maps;signal=service_total;) | [rtc_balancer_core-sat-internal_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sat-internal_maps_yandex_net_sas) <br>[rtc_balancer_core-sat-internal_maps_yandex_net_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sat-internal_maps_yandex_net_vla) |
| Testing | default | [core-sat.testing.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-sat.testing.maps.yandex.net/) | [core-sat.testing.maps.yandex.net](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/itype=balancer;ctype=prod;locations=sas;fqdn=core-sat.testing.maps.yandex.net;prj=core-sat-testing-maps;signal=service_total;) | [rtc_balancer_core-sat_testing_maps_yandex_net_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/rtc_balancer_core-sat_testing_maps_yandex_net_sas) |


## What happens when service is down

- В БЯК, МЯК, НЯК не показывается спутниковая карта.
- [Static API](https://abc.yandex-team.ru/services/maps-core-renderer-staticapi) пятисотит на запросы со слоем sat.

## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/<<yacare-service-name>>/* |
| Ecstatic | /var/log/yandex/maps/ecstatic-agent/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : ```SELECT * FROM hahn.`//home/logfeller/logs/maps-log/1d/{date}` WHERE tskv_format = 'satproxy' ```; |

## How to fix common problems
[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Если загорелись мониторинги, то почти наверняка причина на стороне S3MDS, поэтому:
- потмотрите графики [s3mds panel](https://yasm.yandex-team.ru/template/panel/s3_client/bucket=maps-sat;owner=1971)
- если проблема действительно там, то напишите в чатик https://t.me/joinchat/Bbsak0DREDckUOGhK-m3aw


## Documentation

Полная схема работы сервиса вместе с описанием процедуры публикации находится [здесь](https://wiki.yandex-team.ru/maps/dev/core/factory/deployment/ здесь).

На `%maps_sat` находится кэширующий nginx-сервер. На `%maps_sat_proxy` установлены пакеты `yandex-maps-sat-tileindex` и `yandex-maps-satproxy`.

Пользователь приходит с параметрами `x`, `y`, `z`, `v`, где `v` — версия слоя (равняется версии самого последнего опубликованного релиза). Используя tileindex, `yandex-maps-satproxy` вычисляет версию, с которой был залит тайл, описываемый координатами `x`, `y`, `z`, формирует url для s3mds и возвращает его в nginx посредством ответа `HTTP 305 Use Proxy`. После этого тайл средствами nginx запрашивается из s3mds и возвращается пользователю.

## Known clients
БЯК, МЯК, НЯК, [Static API](https://abc.yandex-team.ru/services/maps-core-renderer-staticapi)


## Ecstatic Datasets
| Stable | Testing |
| ------ | ------- |
| [yandex-maps-sat-tileindex](http://ecstatic.maps.yandex.net/pkg/yandex-maps-sat-tileindex/versions) | [yandex-maps-sat-tileindex](http://core-ecstatic-coordinator.testing.maps.yandex.net/pkg/yandex-maps-sat-tileindex/versions) |
## SLA
[Statbox](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_core_sat?scale=d&_period_distance=30&_incl_fields=1&_incl_fields=7&_incl_fields=30) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_sat.py)


## Persistent Volumes
* /persistent - основной раздел для хранения персистентных данных, сюда ставятся симлинки из:
  * /var/lib/yandex/maps/ecstatic - все данные экстатика
* /logs - логи, сюда ставится симлинка из /var/log


## Firewall macroses
| staging | URL |
|---|---|
| staging | URL |
|---|---|
| Datatesting | [ \_MAPS_CORE_SAT_DATATESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SAT_DATATESTING_RTC_NETS_ ) |
| Datatestingvalidation | [ \_MAPS_CORE_SAT_DATATESTINGVALIDATION_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SAT_DATATESTINGVALIDATION_RTC_NETS_ ) |
| Datavalidation | [ \_MAPS_CORE_SAT_DATAVALIDATION_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SAT_DATAVALIDATION_RTC_NETS_ ) |
| Load | [ \_MAPS_CORE_SAT_LOAD_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SAT_LOAD_RTC_NETS_ ) |
| Stable | [ \_MAPS_CORE_SAT_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SAT_STABLE_RTC_NETS_ ) |
| Testing | [ \_MAPS_CORE_SAT_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_SAT_TESTING_RTC_NETS_ ) |

| destination | puncher |
|-------------|---------|
| s3.mds.yandex.net | https://puncher.yandex-team.ru/tasks?id=5d0b8f590d0795cede81ea92 |
| s3.mdst.yandex.net | https://puncher.yandex-team.ru/tasks?id=5d0b8f200d0795cede81ea91 |

## Regression Stress Testing Configurations
* Регрессионные стрельбы
    * Lunapark: https://lunapark.yandex-team.ru/regress/MAPSBKOFCT
    * Sandbox: https://sandbox.yandex-team.ru/scheduler/15651 https://sandbox.yandex-team.ru/scheduler/15652
    * Тикет: https://st.yandex-team.ru/MAPSBKOFCT-789

## Links
* Аудит безопасности SECAUDIT-3080
