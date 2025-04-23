### Назначение
Известно, что ТС присылают сигналы двигаясь по некоторым ниткам, однако из самих сигналов непонятно по какой нитке двигается ТС, и из какой части нитки пришел тот или иной сигнал. Поэтому требуется "привязывать" эти сигналы к ниткам (выяснять с какой нитки приходят сигналы и из какой ее части).
На данный момент с этой задачей справляется биндер. Он одновременно с приходом сигналов (в онлайн режиме) привязывает их к ниткам. Однако, если известен полный контекст присылаемых ТС сигналов, то можно сильно улучшить качество привязки (оффлайн привязка) сравнительно с онлайн привязкой. Для этого и был создан `offline_binder`

### Входные и выходные данные
Входная таблица должна содержать колонки `clid`, `vehicle_id`, `timestamp`, `vehicle_type`, `route`, `lon` и `lat` и быть отсортирована по `[clid, vehicle_id, timestamp]`.
См. [protobuf message `Signal`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/statistics/info/gt_based_metrics/libs/table_schemas/signal.proto)

Выходная таблица будет содержать `clid`, `vehicle_id`, `trip_id`, `timestamp`, `thread`, `len_from_start` и будет отсортирована по `[clid, vehicle_id, trip_id, timestamp]`.
См. [protobuf message `TrajectoryPoint1D`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/statistics/info/gt_based_metrics/libs/table_schemas/trajectory.proto#L5)

### Алгоритм
Алгоритм offline_binder разбивает все сигналы на "поездки" с одинаковым `route`, `vehicle_type` и некоторыми другими признаками. Далее присваивает каждой поездке свой `trip_id`. При том `trip_id` не совпадают только при равных значениях в колонках из `reduce-by`. В общем же случае они могут совпадать.
Больше про алгоритм можно прочитать [тут](https://wiki.yandex-team.ru/maps/dev/core/masstransit/metrics/mtinfo-metrics/offline-binder/)

### Пример запуска
```
./offline_binder
    --data-mms /var/lib/yandex/maps/ecstatic/data/yandex-maps-mtgpsmodel-production\:v6_19.01.01-0/data.mms
    -i //home/yatransport/mtinfo-metrics/signals/raw/2019-01-01
    -o //home/yatransport/mtinfo-metrics/signals/bound/2019-01-01
```
