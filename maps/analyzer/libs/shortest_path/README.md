# Кратчайшие пути на графе

Библиотека для поиска кратчайших путей на графе. Используется в привязке GPS-сигналов к графу.

Основные заголовочники:
* [`shortest_paths_finder.h`](include/shortest_paths_finder.h) — класс и функции для поиска пути. Если планируется искать много раз в одной окрестности, лучше создать `ShortestPathsFinder`, так как он дополнительно кэширует информацию об исходной и целевой вершинах. Для разового поиска можно просто взять функцию `shortestPath`.
* [`shortest_paths_cache.h`](include/shortest_paths_cache.h) — кэши для переиспользования подсчитанной части алгоритма Дейкстры, а также уменьшения кол-ва обращений к графу. Готовых реализаций две:
    * `ShortestPathsLRUCache` — LRU-кэш, подходит лучшим образом для ситуации, когда матчатся сигналы одного пользователя, так как уже пройденные части становятся неинтересны (пользователь с них уехал и вряд ли вернётся), и их можно удалять из кэша. Используется в оффлайн-привязке на YT, лимитируя кол-во потребляемой джобой памяти.
    * `ShortestPathsThreadedCache` — шардированный LRU-кэш, многопоточный (если `ThreadSafe`, т.е. по умолчанию), подходит для матчинга сразу многих пользователей + по умолчанию настроен на гораздо больший размер. Используется, например, в сервисе [пробок](/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer).

Вспомогательные:
* [`concat.h`](include/concat.h) — конкатенация путей на графе, семейство функций `append*` и `concat*`, а также `adjacent*` для проверки смежности, при этом есть две версии:
    - версия без графа соединит пути только разделяющие общее ребро (т.е. один путь оканчивается на ребре, а другой на нём начинается)
    - версия с графом может соединить через общую вершину
* [`point_on_graph.h`](include/point_on_graph.h) — точка на графе (сегмент + позиция)
* [`types.h`](include/types.h) — синонимы типов для ребра, сегмента, части сегмента и т.п. в трёх ипостасях:
    * `EdgeId`, `SegmentId`... — типы с "коротким" id ребра, именно они используется при поиске
    * `LongEdgeId`, `LongSegmentId`, ... — аналогичные типы с "длинным" (персистентным) id ребра
    * `tpl::EdgeId<T>`, `tpl::SegmentId<T>`, ... — шаблонная версия, выбирающая один из упомянутых вариантов на основе переданного типа id (`EdgeId` или `LongEdgeId`)
* [`convert.h`](include/convert.h) — конвертация из типов с "коротким" id в "длинные" и обратно
* [`path.h`](include/path.h) — тип для описания пути на графе, состоит из:
    * `source` — исходная точка на графе
    * `target` — целевая точка на графе
    * `info` — агрегированная информация о пути
    * `trace` — сам путь (вектор частей сегментов до первой вершины, затем вектор рёбер, а затем вектор частей сегментов до целевой вершины); в результате поиска поле не заполнено, используйте `restorePath` для заполнения.
* [`segment_part_iterator.h`](include/segment_part_iterator.h) — итератор по пути, на каждом шаге в качестве значения `SegmentPart` (или `LongSegmentPart` соот-но). Для прохода используй `iteratePath` из [`path.h`](include/path.h)


## Использование

```cpp
#include <maps/analyzer/libs/shortest_path/include/convert.h>
#include <maps/analyzer/libs/shortest_path/include/shortest_paths_finder.h>

namespace mas = maps::analyzer::shortest_path;

void example() {
    auto cache = std::make_shared<mas::ShortestPathsCache>();
    auto finder = std::make_shared<mas::ShortestPathsFinder>(
        graph,
        cache
    );
    // NOTE: `ShortestPathsFinder` также сам может создать кэш
    // > auto finder = std::make_shared<mas::ShortestPathsCache>(graph, true);
    auto p = finder.find(sourcePoint, targetPoint, 1500.0); // max distance
    if (p) {
        // После поиска в `Path` нет информации о самих сегментах и рёбрах,
        // только агрегированная информация типа "длина пути", "кривизна пути"
        // Для получения самого пути надо позвать функцию `restore`
        finder.restore(*p);
        // Преобразуем в путь с длинными ID рёбер; если версии графа и индекса совпадают
        // это гарантированно удастся
        auto longPath = mas::convertToLong(persistentIndex, *p);
        REQUIRE(longPath, "error converting to long edge ids");

        // Обойдём все сегменты пути
        // Необходимо передавать граф, так как оттуда нужна информация о кол-ве сегментов в рёбрах
        for (auto seg: mas::iteratePath(*longPath, graph, persistentIndex)) {
            std::cout
                << "edge=" << seg.segmentId.edgeId.value()
                << "; segment-index=" << seg.segmentId.segmentIndex.value()
                << "; from " << seg.start << " to " << seg.finish
                << std::endl;
        }
    }
}

```
