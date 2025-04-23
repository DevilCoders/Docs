# Документация market-shops

## Что это?
DataApi-сервис, отдающий информацию о магазине по его идентификатору. Сервис - попытка вынести и актуализировать информацию, связанную с магазинами из репорта.
Данные поставляет MBI. Разрабатывается в рамках [Backbone](https://wiki.yandex-team.ru/market/development/architecture/backbone/)
[Тикет-зонтик](https://st.yandex-team.ru/MARKETTECH-2426)
В настоящий момент сервис отдает информацию по магазину аналогично плейсу productoffers. В будущем планируется доработать до замены плейсов shop_info, shops_list, business_info.

## Где это?
[ABC](https://abc.yandex-team.ru/services/shop)
[Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/uservices/services/market-shops)
[На карте ЦУМа](https://tsum.yandex-team.ru/registry/market-map/service/shop?tab=about)
[Автогенеренный дашборд nginx в графане](https://grafana.yandex-team.ru/d/o4fwnkA7z/market-shop-auto-graph)
[Метрики в соломоне](https://solomon.yandex-team.ru/admin/projects/backbone/metrics)
[Дашборд в мониторинге](https://monitoring.yandex-team.ru/projects/backbone/dashboards/monmb3fe35638phlpdl4?from=now-6h&to=now&refresh=60000&p.smooth=0m&p.percentile=99&p.geo_filter%5B0%5D=sas&p.geo_filter%5B1%5D=vla&p.env_filter=production)
[Релизный пайплайн](https://tsum.yandex-team.ru/pipe/projects/Backbone/delivery-dashboard/shop)
[Сервис в Деплое prod](https://yd.yandex-team.ru/stages/production_market_shop)
[Сервис в Деплое testing](https://yd.yandex-team.ru/stages/testing_market_shop)
[Дашборд алертов backbone](https://juggler.yandex-team.ru/dashboards/backbone)
[Логи в графане](https://nda.ya.ru/t/CjvjKr4P56SeF3)
[Автогенеренная документация из такси](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/market-shops/api/api/)

Балансеры:
http://shop.vs.market.yandex.net
http://shop.tst.vs.market.yandex.net

## Конфигурация
### Прод
Два ДЦ VLA и SAS, по два инстанса
3 CPU, 16Gb RAM, 35Gb HDD (2.3 CPU, 15Gb RAM, 30Gb HDD на box)

### Тестинг
Два ДЦ VLA и SAS, по одному инстансу
2 CPU, 4Gb RAM, 30Gb (HDD 1.3 CPU, 3Gb RAM, 25Gb HDD на box)

### RPS
Продовая нагрузка на плейс productoffers сейчас 4.5К RPS. Работоспособность сервиса при 1 ДЦ подтверждается [стрельбами](https://st.yandex-team.ru/MARKETTECH-2559)
