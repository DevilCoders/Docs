Этой утилитой можно вырезать кусок данных yandex-maps-masstransit-data-rasp, которые попадают в заданный диапазон широты и долготы. По сути эта утилита оставляет остановки, попадающие в нужный регион, и маршруты/нитки, которые проходят только через эти остановки.

Запускать вот так:
```
./filter_data --lat-range 55.571693,55.909857 --lon-range 37.367477,37.843775 -i ~/yandex-maps-masstransit-data-rasp_18.12.11-0/ -o ~/data_rasp
```
Эта команда вырежет из данных кусок примерно соответствующий Москве и положит его в папку data_rasp.

Опция `--outer` позволяет оставить нитки, выходящие за пределы прямоугольника - достаточно, чтобы хотя бы одна остановка лежала внутри.

Если с этими данными хочется запустить роутер, то еще нужно пересобрать часть yandex-maps-pedestrian-graph-fb.
Сначала собираем привязку остановок к пешеходному графу:
```
./build_stops_binding --input data_rasp --fb-graph pedgraph/road_graph.fb -rtree rtree.fb --barriers pedgraph/routing_barriers_rtree.mms.1 --output pedgraph/stops_bindings.fb
```
`data_rasp` - директория с вырезанным yandex-maps-masstransit-data-rasp.
`pedgraph` - директория с пешеходным графом.
`build_stops_binding` - вот эта программа https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/tools/data_build/build-stops-binding?rev=4015975

Потом надо пересчитать пешеходные расстояния между остановками:
```
./build_pedestrian_transfers --mt-data data_rasp --conf pedgraphconf.yaml --dest pedgraph/on_foot_transfers --threads 20
```
Эта программа лежит вот тут https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/tools/data_build/build_pedestrian_transfers
Содержимое `pedgraphconf.yaml` примерно такое:
```
pedestrianGraph:
    dataset_dir: /home/bugsbunny/pedgraph
```
Замечу, что эту команду надо запускать после `build_stops_binding`, т.к. она использует `stops_bindings.fb`.
