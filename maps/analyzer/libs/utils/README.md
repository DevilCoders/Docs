Utils lib
===

Вспомогательные функции. Библиотека не имеет никаких зависимостей.

## Heterogeneous

Гетерогенные `map_each` и `for_each`, т.е. работающие над кортежами.

Пример (см. также [тесты](tests/heterogeneous_test/heterogeneous_test.cpp)):
```cpp
#include <maps/analyzer/libs/utils/include/heterogeneous.h>

auto t = std::tuple{1, "hello", 2.0};
maps::analyzer::for_each(t, [](auto&& v) {
    std::cout << v << std::endl;
});
```

Также есть версии с индексами:
```cpp
auto t = std::tuple{1, "hello", 2.0};
auto t2 = std::tuple{"hm", 3.0, true};
maps::analyzer::for_each_idx(t, [](auto&& v, auto&& idx) {
    auto&& v2 = std::get<std::remove_cvref_t<decltype(idx)>::value>(t2);

    std::cout << "item " << idx << " " << v << " and " << v2 << std::endl;
};
```

## Chain

Аналог питоновского `chain`, проходит по порядку контейнеры. Чтобы указать часть контейнера, можно взять `rangeView`.<br>

NOTE: `std::set` возвращает константные ссылки при итерировании, используй константную версию `cchain` (по аналогии с `begin`/`cbegin`).

Использование (см. также [тесты](tests/chain_test/chain_test.cpp)):
```cpp
#include <maps/analyzer/libs/utils/include/chain.h>
#include <maps/analyzer/libs/utils/include/range_view.h>

std::vector<int> vec{1, 2, 3};
std::list<int> lst{4, 5, 6};
std::set<int> st{7, 8, 9};

// go over 1 2 3 4 5 6
for (const auto& v: maps::analyzer::chain(vec, lst)) {
    std::cout << v << std::endl;
}

// go over 2 3 4 5 6 7 8 9
for (const auto& v: maps::analyzer::cchain( // NOTE: using `cchain` because of `set`
    maps::analyzer::rangeView(vec.cbegin() + 1, vec.cend()), // NOTE: `cbegin` instead of `begin`!
    lst,
    st,
));
```
