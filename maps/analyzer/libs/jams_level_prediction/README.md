Библиотека предсказания пробочных баллов
===

Библиотека описывает основные типы, структуру хранения истории, методы расчета факторов предсказания и методы предсказания пробочных баллов.

Описание интерфеса:
===

C++
==
- [`include/features.h`](include/features.h) – перечисление факторов модели
- [`include/mms_storage.h`](include/mms_storage.h) – описание структуры хранилища истории баллов
- [`include/model.h`](include/model.h) – описание типов модели и ее конфига, методы расчета факторов и предсказания
- [`include/types.h`](include/types.h) – описание вспомогательных типов

Python
==
- [`pylib/operations.py`](pylib/operations.py) – питонячьи функции

Пример использования библиотеки для предсказания
===
Для предсказания используются:
- история пробочных баллов
- геобаза
- [календарь](/arc/trunk/arcadia/maps/analyzer/libs/calendar)

Пример кода:
```cpp
#include <library/cpp/geobase/lookup.hpp>
#include <maps/analyzer/libs/calendar/include/calendar.h>
#include <maps/analyzer/libs/jams_level_prediction/include/mms_storage.h>
#include <maps/analyzer/libs/jams_level_prediction/include/model.h>

namespace jams_level_prediction = maps::analyzer::jams_level_prediction;

const NGeobase::TLookup geobase = ...
const maps::analyzer::calendar::flat_buffers::CalendarStorage calendar = ...
const auto levelHistory = jams_level_prediction::storage::mapStorageFromFile(...);
const auto model = jams_level_prediction::Model::load(...)

const auto currentLevel = ...
const auto currentTime = ...
const auto predictTime = ...
const auto regionId = ...

const auto prediction = jams_level_prediction::predict(
    *model,
    currentLevel,
    currentTime,
    predictTime,
    regionId,
    levelHistory,
    geobase,
    calendar
);
```

Конфигурация модели:
===
Конфигурация модели описывается с помощью файла вида:
```json
{
    "features": [
        "CUR_LEVEL",
        "CUR_TIMESTAMP",
        "AHEAD",
        "AHEAD_HOUR",
        "PREDH_HOUR",
        "PREDH_DAY_OF_MONTH",
        "PREDH_MONTH",
        "PREDH_YEAR",
        "PREDH_DAY_OF_YEAR",
        "PREDH_DAY_OF_YEAR_NORM",
        "PREDH_DAY_TYPE",
        "PREDH_NEXT_DAY_TYPE",
        "PREDH_PREV_DAY_TYPE",
        "PREDH_BEG_LAST_3_AVG",
        "PREDH_BEG_LAST_3_MIN",
        "CURH_BEG_LAST_3_AVG",
        "CURH_BEG_LAST_3_MIN",
        "CURH_AVG_LAST_3_AVG",
        "CURH_AVG_LAST_3_MIN",
        "REGION_ID",
        "COUNTRY_ID",
        "REGION_LAT",
        "REGION_LON",
        "REGION_POPULATION"
    ]
}
```
