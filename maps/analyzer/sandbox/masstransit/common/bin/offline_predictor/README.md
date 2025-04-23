`offline predictor`
===
Редьюсер эмулирует работу сервиса masstransit predictor в оффлайне.
Исходными данными для сервиса являются сырые сигналы общественного транспорта, шаридированные по маршруту.
Данный редьюсер при этом обрабатывает три типа таблиц:
1. ОТ-сигналы с добавлением колонки `NORAMLIZED_ROUTE`, например, [такие](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/dev/users/ovchinkin/MAPSJAMS-3699/2021-09-15/signals_with_normalized_route)
2. road graph traits – таблички [road_graph_traits](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/road_graph_traits), заджойненные с табличкой алиасов (например, [такой](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/dev/users/ovchinkin/MAPSJAMS-3699/2021-09-15/route_aliases)), в результате чего получается, например, [такая табличка](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/dev/users/ovchinkin/MAPSJAMS-3699/2021-09-15/joined_rg_traits)
2. jams – таблички [readtime_jams](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/realtime_jams), заджойненные с табличкой алиасов (например, [такой](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/dev/users/ovchinkin/MAPSJAMS-3699/2021-09-15/route_aliases)), в результате чего получается, например, [такая табличка](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/dev/users/ovchinkin/MAPSJAMS-3699/2021-09-15/joined_jams)

Редьюс происходит по ключам `NORAMLIZED_ROUTE`, `VEHICLE_TYPE`, дополнительно отсортировав записи по времени (`receive_time` для сигналов, `time` для пробок и `0` для rg-traits)

Выходом данного редьюса является таблица с предсказаниями в формате [PREDICTIONS_TABLE](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/masstransit/common/pylib/schema.py?rev=r8566564#L46).
