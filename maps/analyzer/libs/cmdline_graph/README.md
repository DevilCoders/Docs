Парсинг аргументов командной строки для загрузки файлов графа
===

[`maps/analyzer/libs/cmdline_graph/include/cmdline_graph.h`](include/cmdline_graph.h)

Пример использования:
```cpp
#include <maps/analyzer/libs/cmdline_graph/include/cmdline_graph.h>
#include <maps/libs/cmdline/include/cmdline.h>

int main(int argc, char* argv[]) {
    namespace cg = maps::analyzer::cmdline_graph;

    maps::cmdline::Parser p;

    auto s = p.string("arg").help("some arg");
    auto ents = cg::EntitiesLoader(p, {
        cg::Entity::RoadGraph,
        cg::Entity::RTreeFB,
        cg::Entity::EdgesPersistentIndexFB,
    });

    p.parse(argc, argv);

    const auto mappingMode = EMappingMode::Locked;

    const auto roadGraph = ents.load<cg::Entity::RoadGraph>(mappingMode);
    const auto persistentIndex = ents.load<cg::Entity::EdgesPersistentIndexFB>(mappingMode);
    const auto rtree = ents.load<cg::Entity::RTreeFB>(*roadGraph, mappingMode);
    // use them
}
```

`ents.load` возвращает загруженные объекты.
Возвращаемые типы можно увидеть в заголовочном файле в макросах `ENTITY_TYPE`.

Добавить новый объект
===

1. В заголовочном файле [`maps/analyzer/libs/cmdline_graph/include/cmdline_graph.h`](include/cmdline_graph.h) добавить элемент в `enum class Entity`
2. Добавить вызов макроса `ENTITY_TYPE` с аргументами: значение `enum`а, тип, аргументы по умолчанию в конструктор (можно опустить)
3. В [`maps/analyzer/libs/cmdline_graph/impl/cmdline_graph.cpp`](impl/cmdline_graph.cpp) дополнить `INFOS` с полями: значение `enum`а, имя объекта (произвольное), имя файла, имя параметра командной строки, описание для `help`а в командной строке
