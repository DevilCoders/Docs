### Назначение
С траекториями движения по нитке работать неудобно, т.к.
- сложно понимать, насколько близко геометрически одна точка от другой, особенно если они находятся на разных нитках
- постоянно приходится читать геометрию нитки из файлов, когда нужно перейти к геокоординатам или определить момент прибытия на остановку.

Поэтому предлагается преобразовать все траектории из, так называемых, 1D координат в 2D, а также выписать моменты прибытий на остановки, чтобы дальше можно было работать с этими данными без помощи data.mms. Для этого создана `expand_trajectory`. Геометрия ниток читается из data.mms. Для каждой 1D траектории во входной таблице (т.е. набора строк с одинаковым значением в колонках из списка `reduce-by`) добавляются колонки `lon`, `lat` с координатами точек траектории, а также добавляются те вершины (точки) геометрии нитки, через которые проходит траектория. При этом время прохода через новые точки вычисляется линейной интерпояцией времён прохода ближайших точек траектории. Моменты прибытий на остановки записываются в отдельную таблицу.
Преполагается, что после этого этапа в выходных таблицах будет достаточно информации, чтобы не использовать data.mms для дальнейших действий. Стоит отметить, что в результирующих таблицах информация о 1D координатах остаётся, но её использование не предполагается.

### Входные и выходные данные
Входная таблица должна быть отсортирована по `[clid, vehicle_id, trip_id, timestamp]`, и содержать колонки `clid`, `vehicle_id`, `trip_id`, `timestamp`, `thread` и `len_from_start`.
См. [protobuf message `TrajectoryPoint1D`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/statistics/info/gt_based_metrics/libs/table_schemas/trajectory.proto#L5)
Выходная таблица с траекториями будет содержать все те же колонки, а также `lon` и `lat`, а выходная таблица с прибытиями - колонки `clid`, `vehicle_id`, `timestamp`, `thread`, `len_from_start`, `stop_id`.
См. protobuf message [`TrajectoryPoint2D`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/statistics/info/gt_based_metrics/libs/table_schemas/trajectory.proto#L17) и [`Arrival`](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/statistics/info/gt_based_metrics/libs/table_schemas/arrival.proto#L66)

### Пример запуска
```
./expand_trajectory
    --data-mms /var/lib/yandex/maps/ecstatic/data/yandex-maps-mtgpsmodel-production\:v6_18.10.16-0/data.mms
    -i //home/yatransport/mtinfo-metrics/fc/1d/2018-10-17
    -t //home/yatransport/mtinfo-metrics/fc/2d/2018-10-17
    -s //home/yatransport/mtinfo-metrics/fc/arrivals/2018-10-17
```
