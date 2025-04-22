# Quotateka

Quotateka - система управления квотами на использование API сервисов Геоплатформы.

**Документация**: https://docs.yandex-team.ru/quotateka/


## General information
| | |
| ---- | --- |
| Ответственные разработчики | Алексей Хроленко (khrolenko@yandex-team.ru) <br> Алексей Савин (alexey-savin@yandex-team.ru) <br> Андрей Андреев (comradeandrew@yandex-team.ru) |
| Сервис в ABC | [maps-core-quotateka](https://abc.yandex-team.ru/services/maps-core-quotateka/)|
| Исходники | [maps/infra/quotateka](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/quotateka) |
| CI project| [maps-core-quotateka](https://a.yandex-team.ru/projects/maps-core-quotateka/ci/actions/launches?dir=maps%2Finfra%2Fquotateka&id=build) |


## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny | Golovan graphics | Jugglers monitoring checks |
| ------- | ------------- | -------------- | ----------------- |
| Stable | [maps_core_quotateka_stable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_quotateka_stable/) | [ core-quotateka.stable ](https://yasm.yandex-team.ru/template/panel/maps-core-quotateka-stable-panel-main/) | [ maps_core_quotateka_stable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_quotateka_stable) |
| Prestable | [maps_core_quotateka_prestable](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_quotateka_prestable/) | [ core-quotateka.prestable ](https://yasm.yandex-team.ru/template/panel/maps-core-quotateka-prestable-panel-main/) | [ maps_core_quotateka_prestable ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_quotateka_prestable) |
| Load | [maps_core_quotateka_load](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_quotateka_load/) | [ core-quotateka.load ](https://yasm.yandex-team.ru/template/panel/maps-core-quotateka-load-panel-main/) | [ maps_core_quotateka_load ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_quotateka_load) |
| Testing | [maps_core_quotateka_testing](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_quotateka_testing/) | [ core-quotateka.testing ](https://yasm.yandex-team.ru/template/panel/maps-core-quotateka-testing-panel-main/) | [ maps_core_quotateka_testing ](https://juggler.yandex-team.ru/aggregate_checks/?query=host%3Dmaps_core_quotateka_testing) |


[Alerts all (tag=a_prj_maps-core-quotateka)](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Da_prj_maps-core-quotateka)


### Balancers

- **Stable**
    - `core-quotateka.maps.yandex.net`
        - [AWACS dashboard](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-quotateka.maps.yandex.net/)
        - [Graphics](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-quotateka-server.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-quotateka-server-maps;signal=service_total)

    - `core-quotateka-server.maps.yandex.net` (dns alias: `core-quotateka-abcd.maps.yandex.net`)
        - [AWACS dashboard](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-quotateka-server.maps.yandex.net/)
        - [Graphics](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-quotateka.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-quotateka-maps;signal=service_total)

- **Testing**
    - 'core-quotateka.common.testing.maps.yandex.net'
    - 'core-quotateka-abcd.common.testing.maps.yandex.net'
    - 'core-quotateka-server.testing.maps.yandex.net'
        - [AWACS dashboard](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/core-quotateka-server.testing.maps.yandex.net/)
        - [Graphics](https://yasm.yandex-team.ru/template/panel/balancer_common_panel/fqdn=core-quotateka-server.testing.maps.yandex.net;itype=balancer;ctype=prod;locations=man,sas,vla;prj=core-quotateka-server-testing-maps;signal=service_total)


### MDB

**Stable**: PostgreSQL `s2.small` x3 instances | [Dashboard](https://yc.yandex-team.ru/folders/aku8ev7m1ilfkviuj5ku/managed-postgresql/cluster/mdb1moscd4bqodo92p2r) | [Graphics](https://monitoring.yandex-team.ru/projects/internal-mdb/dashboards/monukr7hiocljvpn72hb/view?p.cluster=mdb1moscd4bqodo92p2r)

**Load**: PostgreSQL `s2.small` x3 instances | [Dashboard](https://yc.yandex-team.ru/folders/aku8ev7m1ilfkviuj5ku/managed-postgresql/cluster/mdb1oi5assiperjocfp7) | [Graphics](https://monitoring.yandex-team.ru/projects/internal-mdb/dashboards/monukr7hiocljvpn72hb/view?p.cluster=mdb1oi5assiperjocfp7)


**Testing**: PostgreSQL `s2.micro` x3 instances | [Dashboard](https://yc.yandex-team.ru/folders/aku8ev7m1ilfkviuj5ku/managed-postgresql/cluster/mdbv00q8eji7bfs08kaf) | [Graphics](https://monitoring.yandex-team.ru/projects/internal-mdb/dashboards/monukr7hiocljvpn72hb/view?p.cluster=mdbv00q8eji7bfs08kaf)


### Firewall macroses

| Staging | Racktables URL |
|---|---|
| stable | [ \_MAPS_CORE_QUOTATEKA_STABLE_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_QUOTATEKA_STABLE_RTC_NETS_ ) |
| testing | [ \_MAPS_CORE_QUOTATEKA_TESTING_RTC_NETS_ ]( https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_MAPS_CORE_QUOTATEKA_TESTING_RTC_NETS_ ) |


### Persistent Volumes
* /logs - логи, сюда ставится симлинка из /var/log


## Logs
| Name | URL/path |
|---|---|
| Nginx | /var/log/nginx/* |
| Yacare service | /var/log/yandex/maps/quotateka/* |
| Supervisord | /var/log/supervisor/* |
| Syslog (unfiltered) | /var/log/syslog |
| YT  | https://yql.yandex-team.ru : SELECT * FROM hahn.`logs/maps-log/1d/2019-08-20` WHERE vhost LIKE 'core-quotateka.maps.yandex.net' limit 1; |


## Known clients
- [maps-core-driving-router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/routing/router)
- [maps-core-masstransit-router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/router)
- [maps-core-bicycle-router](https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/router)

## What happens when service is down

- Не работает управление аккаунтами и квотами через ABCD и Quotateka web UI
- На хостах провайдеров горит алерт `quotateka-agent-inventory-age` (агенты не получают обновления квот, но продолжают применять старые значения)

### Troubleshooting

[What can go wrong in RTC](https://wiki.yandex-team.ru/users/imseleznev/whatcangowronginrtc)

Для диагностики агента квотатеки есть [документация](https://docs.yandex-team.ru/quotateka/agent_troubleshooting#monitoringi-i-diagnostika-nepoladok)

Для диагностики проблем на бэкенде читать лог: `/var/log/yandex/maps/quotateka/quotateka.log`

## SLA

[Datalens SLA dashboard](https://datalens.yandex-team.ru/hckadjiuwrf8a-maps-sla-dashboard?state=90762bf4145) <br>
[Config](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_core_quotateka.py)

## Regression Testing

* Lunapark chart: https://lunapark.yandex-team.ru/regress/GEOINFRA?service=maps-core-quotateka
* Ticket with configuration details: https://st.yandex-team.ru/GEOINFRA-2556
* Imbalance shooting scheduler: https://sandbox.yandex-team.ru/scheduler/44785/view
* Constant shooting scheduler: https://sandbox.yandex-team.ru/scheduler/44788/view
