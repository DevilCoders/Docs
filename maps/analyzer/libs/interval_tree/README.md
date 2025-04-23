Дерево интервалов
===

https://en.wikipedia.org/wiki/Interval_tree

Контейнер, хранящий объекты с интервалом, и по интервалу возвращающий объекты с интервалами, его пересекающими.<br>
Построение: NlogN, запросы: logN + M (кол-во объектов в результате).<br>
Модификация дерева не поддерживается.

**NOTE**: Границы интервала включаются в интервал, т.о. можно вставить и точку - как пустой интервал.

### Использование

См. также пример в [тестах](tests/interval_tree_test.cpp).

```cpp
#include <maps/analyzer/libs/interval_tree/include/interval_tree.h>

struct Animation {
    int start; int end; // interval is `[start; end]` (not `[start, end)`)
    AnimationData data;
};

std::vector<Animation> objects = createObjects();

auto itree = maps::analyzer::interval_tree::intervalTree(
    // NOTE: objects will be stored inside tree
    // You may also pass iterators pair, but note - objects will be moved into tree too
    // to avoid this, use `cbegin` & `cend`
    std::move(objects),
    // return range - anything deconstructable to pair via `auto [from, to] = ...`
    // i.e. `tuple`, `pair`, simple struct
    [](const Animation& a) { return std::pair{a.start, a.end}; }
);

// iterate over all objects at point 10
for (const auto& a: itree.contains(10)) {
    // ...
}

// iterate over all objects intersected range 10-20
for (const auto& a: itree.intersects(10, 20)) {
    // ...
}
```
