# maps-core-search-billboards

[TOC]


## General information

Serves advertising pins and billboards along the route for mobile clients.
Serves zerospeed and via-banners.

[Wiki-page with more detailed information](https://wiki.yandex-team.ru/users/folunin/core-search-billboards/)

|  |  |
| --- | ----- |
| Call in case of obscurity | [Петр Лежанкин](https://staff.yandex-team.ru/lepetrandr), [Виктор Теплов](https://staff.yandex-team.ru/grok) |
| Sources | https://a.yandex-team.ru/arc/trunk/arcadia/maps/search/advert/basesearch |
| Service in ABC | https://abc.yandex-team.ru/services/maps-core-search-billboards |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks | Balancers |
| ------- | ------------- | -------------- | ----------------- |-----------|
| stable | [addrs_advert_yp][addrs_advert_yp] | [maps-mobile-search](https://yasm.yandex-team.ru/panel/maps-mobile-search) | мобильная прокси ? | [maps-advert.yandex.ru][maps-advert.yandex.ru] |
| prestable | [addrs_advert_prestable_yp][addrs_advert_prestable_yp] | | | |
| testing | [addrs_advert_r1_yp][addrs_advert_r1_yp] |  | | [maps-advert.n.yandex-team.ru](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-adv) |

В общекарточный чат завернуты мониторинги от мобильной прокси и некоторые внутренние.
Отдельные мониторинги на свежесть данных приходят ответственным за данные.

### Balancers

#### Stable
|  desc | link | 
| ----- | ---- | 
| L3-L7 balancers in nanny | [maps-advert.yandex.ru][maps-advert.yandex.ru] | 
| l3manager | https://l3.tt.yandex-team.ru/service/1749 | 
| racktables | https://racktables.yandex-team.ru/index.php?page=ipv4rspool&pool_id=8159 | 
| common metrics | https://yasm.yandex-team.ru/template/panel/balancer_common_panel/prj=maps-advert/ | 
| portoinst metrics | https://yasm.yandex-team.ru/template/panel/balancer_portoinst_panel/prj=maps-advert/ | 
| файрвол puncher | https://puncher.yandex-team.ru/?destination=maps-advert.yandex.ru&rules=exclude_rejected&values=all&sort=destination | 

#### Testing

|  desc | link |
| ----- | ---- |
| L3-L7 balancers in nanny | [maps-advert.n.yandex-team.ru](https://nanny.yandex-team.ru/ui/#/services/balancers/list/production/sections/list/maps-adv) |
| TODO  |.     |


### Balancers urls

* Stable: http://maps-advert.yandex.ru/
* Testing: http://maps-advert.n.yandex-team.ru/

## SLA
  * Criteries: https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/monitoring/sla_calculator/core/services/maps_mobile_billboards.py
  * Statbox: [maps_mobile_billboards](https://stat.yandex-team.ru/Maps_Plus_Beta/SLA/maps_mobile_billboards?scale=d&_incl_fields=d1&_incl_fields=d30&_incl_fields=d7&_period_distance=30)


## Known clients

* [mobile proxy](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/maps_mobile/)


## Logs

| Name | URL/path |
| ---- | -------- |
| [YT](https://yql.yandex-team.ru) | [//logs/maps-search-advert-billboards-response/](https://yt.yandex-team.ru/hahn/navigation?path=//logs/maps-search-advert-billboards-response) |
| TODO | |


## Regression Stress Testing Configurations
TODO

[addrs_advert_yp]: https://nanny.yandex-team.ru/ui/#/services/catalog/addrs_advert_yp
[addrs_advert_prestable_yp]: https://nanny.yandex-team.ru/ui/#/services/catalog/addrs_advert_prestable_yp
[addrs_advert_r1_yp]: https://nanny.yandex-team.ru/ui/#/services/catalog/addrs_advert_r1_yp
[maps-advert.yandex.ru]: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/maps-advert.yandex.ru/show
