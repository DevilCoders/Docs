Эта библиотека предназначена для чтения и записи статических данных общественного транспорта. Данные хранятся во flatbuffer-е, формат данных описан в *.fbs64 файлах, точка входа - [storage.fbs64](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/impl/fb/storage.fbs64)

# Чтение/запись

Точка входа для записи - класс `PredictorDataStorageBuilder` в файле [storage_builder.h](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/include/fb/storage_builder.h). Класс записывает в файл или stream целый объект `PredictorDataContainer`

Точка входа для чтения - класс `PredictorDataStorageReader` в файле [storage_reader.h](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/include/fb/storage_reader.h). У класс есть интерфейс обращения к полям flatbuffer-а и он читает их по мере обращения. Аналогично, при вызове `PredictorDataStorageReader::getThreadInfo` структура `ThreadInfo` не читается целиком, класс `ThreadInfo` читает отдельные атрибуты нитки при обращении к ним

В большинстве случаев более удобно для чтения/записи использовать функции `loadPredictorData` и `flushPredictorDataToFile`, описанные в [predictor_data.h](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/include/predictor_data.h).

Детали реализации reader-ов и writer-ов для каждой конкретной сущности прячутся в пространствах имён `maps::masstransit::predictor_data::flat_buffers::readers` и `maps::masstransit::predictor_data::flat_buffers::writers` соответственно.

# PredictorData

`table PredictorData` в [storage.fbs64](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/impl/fb/storage.fbs64) хранит три структуры:

* threads - вектор структур `ThreadInfo`
* threadMap - хэшмап из `Id` нитки (сейчас это просто строка) в индекс нитки в `threads`
* routeAlias - хэшмап из `RouteId` маршрута (тоже просто строка) в вектор структур `RouteAlias`

`RouteAlias` хранит в себе альтернативные названия маршрутов, которые используют поставщики. См. [формат данных ОТ](https://wiki.yandex-team.ru/maps/dev/core/masstransit/data/dataformatlocaltime/#aliasessinonimy)

Описания всех используемых типов и структур лежат в [types.h](/arc/trunk/arcadia/maps/masstransit/info/libs/predictor_data/include/types.h)

# Атрибуты ниток
Узнать характеристики любой нитки можно при помощи метода `PredictorDataStorageReader::getThreadInfo`. Методы класса `ThreadInfo` возвращают значения отдельных свойств нитки.

| Название метода | Описание |
| --------------- | -------- |
| `id` | Id нитки (строка) |
| `routeId` | Id маршрута (строка). Используется как ключ в `RouteAliasMap` |
| `routeDefaultName` | TODO: добавить описание |
| `vehicleType` | Тип транспортного средства. См. [формат данных ОТ](https://wiki.yandex-team.ru/maps/dev/core/masstransit/data/dataformatlocaltime/#dopustimyetipymarshrutov) |
| `boundingBox` | Минимальный bbox, содержащий геометрию нитки|
| `regionId` | Регион, округленный до уровня 6(Город). См. [документацию libgeobase](https://doc.yandex-team.ru/lib/libgeobase5/concepts/region-types.html) |
| `type` | Linear/Circular |
| `length` | Длина в метрах |
| `edges` | Вектор рёбер, на которые нитка разбивается сегментацией |
| `stages` | Список стейджей. Стейдж это - участок нитки между двумя соседними остановками |
| `schedules` | Вектор расписаний движения транспорта по нитке |

# Рёбра
Сейчас разбиение нитки на рёбра выполняется [сегментатором](/arc/trunk/arcadia/maps/masstransit/info/libs/common/segmentation.h?rev=r7821484#L93). Его текущая реализация делает примерно следующее: нарезает геометрию каждого стейджа на куски по 160 метров, плюс добавляет кусочки по 25 метров вокруг остановок.

Для удобного использования пробок в предсказании времени проезда автобуса по нитке каждое ребро матчится на дорожный граф

Атрибуты ребёр хранятся в классе `EdgeInfo`

| Название метода | Описание |
| --------------- | -------- |
| `type` | Тип ребра из сегментатора ([`StopSegment`, `StageSegment`, `StopPointSegment`](/arc/trunk/arcadia/maps/masstransit/info/libs/common/segmentation.h?rev=7821081#L58)) |
| `geometry` | Геометрия |
| `length` | Длина в метрах |
| `threadOffset` | Расстояние (вдоль полилинии нитки, а не кратчайшее) в метрах от начала нитки до начала ребра |
| `stageIndex` | Индекс стейджа в векторе `ThreadInfo::stages`, которому принадлежит ребро |
| `rgSegmentChain` | Результат привязки ребра к дорожному графу<br><br> Структура `RoadGraphSegmentChain` содержит список рёбер графа и точки начала и конца на крайних рёбрах. Для удобного использования метод `RoadGraphSegmentChain::segments()` возвращает итератор по сегментам дорожного графа |

# Стейджи и остановки
Стейдж это - участок нитки между двумя соседними остановками.

класс `StageInfo` содержит ровно две остановки (`StopInfo`) - начало и конец стейджа

Атрибуты остановок хранятся в классе `StopInfo`

| Название метода | Описание |
| --------------- | -------- |
| `stopIndex` | Индекс остановки на нитке, описан вот [тут](/arc/trunk/arcadia/maps/masstransit/libs/data/reader/include/thread_stop.h?rev=r9064609#L35). Пара `<thread_id, stop_index>` может использоваться как уникальный идентификатор остановки |
| `edgeIndex` | Индекс ребра в векторе `ThreadInfo::edges`, на котором лежит остановка |
| `arrivalTime` | TODO: добавить описание  |
| `departureTime` | TODO: добавить описание |

# Расписания
Статическое расписание движения транспортного средства по маршруту сейчас хранится в классе `ScheduleEntry`.
Документацию про расписания можно посмотреть [тут](https://wiki.yandex-team.ru/maps/dev/core/masstransit/data/dataformatlocaltime/#frequency)

| Название метода | Описание |
| --------------- | -------- |
| `bounds` | Пара из двух `time_t` - начало и конец временного интервала расписания |
| `frequency` | Время между последовательными прибытиями транстпортного средства (в секундах) |

