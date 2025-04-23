Перенос признаков road graph на ОТ ребра.
---

Создает одну табличку на день.<br>
Для каждого ОТ ребра подсчитываются характеристики из road_graph, используя разложение ОТ ребра на последовательность сегментов и ребер из road_graph.
Считаются такие характеристики как:
* число светофоров на ребре
* протяженность ребра (в road_graph'ной геометрии)
* коэффициент покрытия ОТ ребра сегментами из road_graph (`covered_ratio`)
* длина выделенной полосы, которая покрывает ребро
* максимальное ограничение скорости, которое действует на ребре
* средняя скорость движения по ребру

Использует маппинги mt_edge -> rg_edges и road_graph.fb.

### Результаты

Testing: [//home/maps/jams/testing/masstransit/jams](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/masstransit/rg_traits)<br>
Production: [//home/maps/jams/production/masstransit/jams](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/rg_traits)
