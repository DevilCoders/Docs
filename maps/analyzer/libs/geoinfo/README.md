# Геобаза на костылях

Обёртка над [геобазой](library/cpp/geobase) с использованием [`coverage`](/arc/trunk/arcadia/maps/libs/coverage) для определения ID региона по точке.<br>
Геобаза порой выдаёт некорректные результаты, а в [`coverage`](/arc/trunk/arcadia/maps/libs/coverage) нет вспомогательной информации. Данная библиотека их объединяет.
Также имеются [python-биндинги](/arc/trunk/arcadia/maps/analyzer/pylibs/geoinfo) и [YQL UDF](/arc/trunk/arcadia/yql/udfs/maps/geoinfo)<br>
Однако стоит иметь в виду, что `geoid` (`coverage`) менее подробный, чем геобаза.<br>
Если надо добавить какой-то регион, стоит обращаться к tail@

## Описание

В библиотеке имеются два класса:
* [`GeoId`](include/geoid.h) — получение ID региона по координате. Использует только `coverage`.
* [`GeoInfo`](include/geoinfo.h) — получение ID региона с возможностью "округления" до определённого уровня, а также получения различной информации о регионе.

## Примеры

См. также [тесты](tests/geoinfo_test.cpp).

```cpp
#include <maps/analyzer/libs/geoinfo/include/geoinfo.h>

maps::geoinfo::GeoInfo geo(
    "~/arcadia/maps/analyzer/data/coverage/geoid.mms.1",
    "~/arcadia/maps/analyzer/data/geobase/geodata5.bin"
);

auto regionId = geo.regionIdAt({50.0, 30.0});
auto countryId = geo.regionIdAt({50.0, 30.0}, maps::geoinfo::RegionType::COUNTRY);

auto region = geo.regionAt({50.0, 30.0}, maps::geoinfo::RegionType::CITY);
auto name = region.GetName();
```
