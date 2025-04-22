# maps-core-search-billboards (indexer)

[TOC]


## General information

Indexes data for maps-core-search-billboards.
Polls sandbox resource TYCOON_ADS every minute, updates and indexes it if contents is changed.

|  |  |
| --- | ----- |
| Call in case of obscurity | [Петр Лежанкин](https://staff.yandex-team.ru/lepetrandr), [Виктор Теплов](https://staff.yandex-team.ru/grok) |
| Sources | https://a.yandex-team.ru/arc/trunk/arcadia/maps/search/advert/indexer |
| Service in ABC | https://abc.yandex-team.ru/services/maps-core-search-billboards |

## Service infrastructure

### Instances, graphics, monitorings

| Staging | Nanny service | Graphics panel | Monitoring checks | Balancers |
| ------- | ------------- | -------------- | ----------------- |-----------|
| stable | [addrs_advert_indexer_yp](https://nanny.yandex-team.ru/ui/#/services/catalog/addrs_advert_indexer_yp/) | [maps-mobile-search](https://yasm.yandex-team.ru/panel/maps-mobile-search) | TODO | - |
| testing | [addrs_advert_indexer_r1_yp](https://nanny.yandex-team.ru/ui/#/services/catalog/addrs_advert_indexer_r1_yp/) |  | | - |

Мониторинги на свежесть данных приходят ответственным за данные.

## Known clients

* [maps_mobile_billboards](https://wiki.yandex-team.ru/geo-infra/Tablica-otvetstvennyx-za-geo-servisy/maps_mobile_billboards/)

