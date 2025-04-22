# Геобаза на костылях

Биндинги к C++ библиотеке [`geoinfo`](/arc/trunk/arcadia/maps/analyzer/libs/geoinfo). Также есть [YQL UDF](/arc/trunk/arcadia/yql/udfs/maps/geoinfo).

## Описание

В библиотеке имеются два класса:
* [`PyGeoId`](geoid.pyx) — получение ID региона по координате. Использует только `coverage`.
* [`PyGeoInfo`](geoinfo.pyx) — получение ID региона с возможностью "округления" до определённого уровня, а также получения различной информации о регионе.

## Пример

См. также [тесты](tests/test_geoinfo.py).

```python
import maps.analyzer.pylibs.geoinfo as geoinfo

geo = geoinfo.PyGeoInfo(
    "~/arcadia/maps/analyzer/data/coverage/geoid.mms.1",
    "~/arcadia/maps/analyzer/data/geobase/geodata5.bin",
)

region_id = geo.region_id_at(50.0, 30.0)
country_id = geo.region_id_at(50.0, 30.0, geoinfo.RegionType.COUNTRY)

region = geo.region_at(50.0, 30.0, geoinfo.RegionType.CITY)
name = region['name']
```
