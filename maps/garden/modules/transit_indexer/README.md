# Модуль подготовки данных для поиска по ОТ

Данный модуль <b>transit_indexer</b> с помощью [индексатора](https://a.yandex-team.ru/arc/trunk/arcadia/maps/search/transit/indexer) подготавливает данные для сервиса [поиска по общественному транспорту](https://wiki.yandex-team.ru/users/timofey/masstransit-search/architecture/) и заливает в сэндбокс ресурс [MAPS_TRANSIT_INDEX](https://sandbox.yandex-team.ru/resources?type=MAPS_TRANSIT_INDEX&limit=20&created=14_days).

Также производится деплой полученного ресурса в один из сервисов в Няне в зависимости от окружения - [maps_core_transit_datavalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_transit_datavalidation/) либо [maps_core_transit_datatestingvalidation](https://nanny.yandex-team.ru/ui/#/services/catalog/maps_core_transit_datatestingvalidation/).
