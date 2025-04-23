# Генератор датасетов слоя "Зеркал"

## Датасеты экспорта

### ecstatic
| Stable | Datatesting |
| ------ | ------- |
| [yandex-maps-mrc](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc/versions) | [yandex-maps-mrc](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc/versions) |
| [yandex-maps-mrc-activation](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-activation/versions) | [yandex-maps-mrc-activation](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-activation/versions) |
| [yandex-maps-mrc-features-secret](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-features-secret/versions) | [yandex-maps-mrc-features-secret](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-features-secret/versions) |
| [yandex-maps-mrc-graph](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-graph/versions) | [yandex-maps-mrc-graph](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-graph/versions) |
| [yandex-maps-mrc-graph-pro](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-graph-pro/versions) | [yandex-maps-mrc-graph-pro](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-graph-pro/versions) |
| [yandex-maps-mrc-pedestrian-graph](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph/versions) | [yandex-maps-mrc-pedestrian-graph](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph/versions) |
| [yandex-maps-mrc-pedestrian-graph-pro](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph-pro/versions) | [yandex-maps-mrc-pedestrian-graph-pro](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-pedestrian-graph-pro/versions) |
| [yandex-maps-mrc-photo-to-edge](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-edge/versions) | [yandex-maps-mrc-photo-to-edge](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-edge/versions) |
| [yandex-maps-mrc-photo-to-edge-pro](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-edge-pro/versions) | [yandex-maps-mrc-photo-to-edge-pro](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-edge-pro/versions) |
| [yandex-maps-mrc-photo-to-pedestrian-edge](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-pedestrian-edge/versions) | [yandex-maps-mrc-photo-to-pedestrian-edge](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-pedestrian-edge/versions) |
| [yandex-maps-mrc-photo-to-pedestrian-edge-pro](http://ecstatic.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-pedestrian-edge-pro/versions) | [yandex-maps-mrc-photo-to-pedestrian-edge-pro](http://core-ecstatic-coordinator.datatesting.maps.yandex.net/pkg/yandex-maps-mrc-photo-to-pedestrian-edge-pro/versions) |

### Описание
 - `yandex-maps-mrc` - все опубликованные фотографии, за исключением приватных
 - `yandex-maps-mrc-activation` - синхронизирующий датасет
 - `yandex-maps-mrc-features-secret` - все опубликованные приватные фотографии
 - `yandex-maps-mrc-graph` - актуальное покрытие автомобильного графа фотографиями, за исключением приватных
 - `yandex-maps-mrc-graph-pro` - включая приватные снимки
 - `yandex-maps-mrc-pedestrian-graph` - актуальное покрытие пешеходного графа фотографиями, за исключением приватных
 - `yandex-maps-mrc-pedestrian-graph-pro` - включая приватные снимки
 - `yandex-maps-mrc-photo-to-edge` - связь фотографий с ребрами автомобильного графа
 - `yandex-maps-mrc-photo-to-edge-pro` - включая приватные снимки
 - `yandex-maps-mrc-photo-to-pedestrian-edge` - связь фотографий с ребрами пешеходного графа
 - `yandex-maps-mrc-photo-to-pedestrian-edge-pro` - включая приватные снимки

### Формат
Все датасеты сериализуются во flatbuffers с помощью библиотек:
- [fb](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/libs/fb)
- [fb_rtree](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/libs/fb_rtree)

### Версии
Версии датасетов имеют формат `YY.MM.DD-millis`, где `millis` число миллисекунд прошедших после полуночи.

## Алгоритм экспорта

### Основные этапы

![alt text](https://jing.yandex-team.ru/files/naplavkov/graphviz-2.svg)

<details><summary>graphviz</summary><pre><code>

digraph G {

    subgraph cluster_features {
        style=filled
        color=lightgrey
        node [style=filled,color=white]
        generateFbFeatures -> Photos
        label = "экспорт фотографий"
    }

    subgraph cluster_relations {
        style=filled
        color=lightgrey
        node [style=filled,color=white]
        findPrevEdgePhotosIfActual -> match -> evalEdgePhotos -> EdgePhotos
        findPrevEdgePhotosIfActual -> EdgePhotos
        label = "экспорт связей 'фотография-ребро'"
    }

    subgraph cluster_coverages {
        style=filled
        color=lightgrey
        node [style=filled,color=white]
        findPrevEdgeIfActual -> makeEdgeCoverage -> TEdges
        findPrevEdgeIfActual -> TEdges
        label = "экспорт покрытий"
    }

    features [label="yandex-maps-mrc[-features-secret]",shape=folder,color=red,style=filled,fillcolor=orange]
    relations [label="yandex-maps-mrc-photo-to[-pedestrian]-edge[-pro]",shape=folder,color=red,style=filled,fillcolor=orange]
    coverages [label="yandex-maps-mrc[-pedestrian]-graph[-pro]",shape=folder,color=red,style=filled,fillcolor=orange]
    database  [label="postgres",shape=cylinder,color=blue,style=filled,fillcolor=lightblue]
    Photos  [shape=box]
    findPrevEdgePhotosIfActual  [shape=diamond]
    EdgePhotos  [shape=box]
    findPrevEdgeIfActual  [shape=diamond]
    TEdges  [shape=box]

    Photos -> findPrevEdgePhotosIfActual
    generateFbFeatures -> features
    EdgePhotos -> findPrevEdgeIfActual
    EdgePhotos -> relations
    TEdges -> coverages

    features -> generateFbFeatures [color=red]
    relations -> findPrevEdgePhotosIfActual [color=red]
    coverages -> findPrevEdgeIfActual [color=red]

    database -> generateFbFeatures [color=blue]
    database -> match [color=blue]

}

</code></pre></details>

### Экспорт фотографий
- вход: БД (db::Features, db::ObjectsInPhoto, db::WalkObjects) и датасеты от предыдущего запуска (обратная связь - см. выход)
- выход: датасеты ```yandex-maps-mrc[-features-secret]```, [Photos](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/export_gen/lib/tools.h?rev=r8871626#L35)

### Экспорт связей 'фотография-ребро'
- вход: [Photos](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/export_gen/lib/tools.h?rev=r8871626#L35), БД (db::TrackPoints) и датасеты от предыдущего запуска (обратная связь - см. выход)
- трек фотографий привязывается к графу библиотекой [graphmatching](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/libs/graphmatching)
- связь устанавливается если привязанный трек проходит через ребро графа
- расстояние до первого ребра, длина "видимого" пути и отклонения направлений отрезков ребер ограничены
- ограничения могут приводить к пустым связям (```begin() == end()```) - во избежание повторного матчинга
- выход: датасеты ```yandex-maps-mrc-photo-to[-pedestrian]-edge[-pro]```, [EdgePhotos](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/export_gen/lib/graph.cpp?rev=r8896234#L30)

### Экспорт покрытий
- вход: [EdgePhotos](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/mrc/long_tasks/export_gen/lib/graph.cpp?rev=r8896234#L30) и датасеты от предыдущего запуска (обратная связь - см. выход)
- выход: датасеты ```yandex-maps-mrc[-pedestrian]-graph[-pro]```
