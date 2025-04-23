Библиотека для работы со статистическими данными для whole track model
===

В библиотеке описаны основные типы для работы со статистическим данными проездов по ребрам графа. Эти данные используются для расчета фич, используемых в whole track model.

- [`statistical_interval.h`](include/statistical_interval.h) – описывает интервал, за который расчитаны статистики
- [`statistical_data.h`](include/statistical_data.h) – описывает данные, которые могут быть получены для заданного интервала

Также имеются вспомагательные инструменты к вышеописанным типам:
- [`constants.h`](include/constants.h) – константы, необходимые для работы библиотеки

Директория /storage библиотеки описывает процесс сериализации, десериализации статистик в flat buffer, а также функции для получения нужных статистик.

Хранилище([`storage.h`](include/storage/storage.h)) состоит из следующих структур:

1. _map__ - мапа на основе кодирования Элиаса-Фано([`persistent_id_map.h`](include/storage/persistent_id_map.h)), в которой ключ - persistent_id, а значение представляет собой битовую маску интервалов и стартовое смещение в массиве из пункта 2. Каждый бит в битовой маске описывает наличие или отсутсутвия интервала*. Таким образом, если у нас есть интервал, мы можем найти сколько интервалов(бит) присутствуют до него. Умножив это количество интервалов на число статистик и прибавив стартовое смещение, мы сможем найти смещение в массиве из пункта 2, начиная с которого записаны нужные статистики.
2. _stats__ - массив состоящий из сжатых значений статистик

Идея поиска по _persistent_id_ и интервалу соответсвующих статистик в следующем:

- Используем мапу для поиска битовой маски интервалов
- По битовой маске интервалов и самому интервалу находим количество интервалов, предшествующих нашему*, для которых в массиве статистик есть данные. Находим смещение в массиве статистик
- По смещению находим нужные статистики и распаковываем их

\* Интервалы нумеруются в лексикографическом порядке.

Номер интервала | Лексикографическое предствление | Чему соответсвует
--- | --- | ---
0 | "" | пустой интервал, соответсвующий всему периоду агрегации
1 | "0" | первый день
2 | "0\_00" | первый час первого дня
3 | "0\_00\_0" | первая четверть первого часа первого дня
4 | "0\_00\_1" | вторая четверть первого часа первого дня
5 | "0\_00\_2" | третья четверть первого часа первого дня
6 | "0\_00\_3" | четвертая четверть первого часа первого дня
7 | "0\_01" |  второй час первого дня
8 | "0\_01\_0" | первая четверть второго часа первого дня
... | ... | ...
121 | "0\_23\_3" | третья четверть двадцать четвертого часа первого дня
122 | "1" | второй день
... | ... | ...

Пример чтения данных:
===
```cpp
#include <maps/analyzer/libs/jams_statistical_data_4/include/storage/storage.h>

std::string mmsFile = ...
std::string time = ...
uint64_t persistentId = ...

using namespace maps::analyzer::jams_statistical_data_4;
namespace ma = maps::analyzer;

const storage::JamsStatisticalStorage storage(fb_file, false /* populate */, false /* lock memory */);

const auto info = storage.getEdgeIntervalStatisticalData(
    persistentId,
    shortestIntervalForTime(time)
);

if (info) {
    std::cout << "interval: ";
    if (info->intervalDuration) {
        std::cout << *info->intervalDuration;
    } else {
        std::cout << "–";
    }
    std::cout
        << ", count: " << info->count
        << std::fixed << std::setprecision(5)
        << ", speedMin: " << info->speedMin
        << ", speedMax: " << info->speedMax
        << ", speedAvg: " << info->speedAvg
        << ", speedP50: " << info->speedP50;
} else {
    std::cout << "no info";
}

std::cout << std::endl;

```

Пример создания данных:
===
```cpp
#include <maps/analyzer/libs/jams_statistical_data_4/include/fb/storage.h>

using namespace maps::analyzer::jams_statistical_data;
namespace ma = maps::analyzer;

std::string outputPath = ... // read from options

auto reader = ma::createYSONReader();
if (!reader->IsValid()) {
    return 0;
}

storage::JamsStatisticalStorageBuilder builder;

while(reader->IsValid()) {
    const auto& row = reader->GetRow();
    builder.push(row);
    reader->Next();
}

builder.writeToFile(outputPath);
```
