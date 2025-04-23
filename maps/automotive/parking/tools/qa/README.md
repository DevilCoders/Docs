# Набор инструментов для оценки качества определения парковок

## parking_detector

Модуль для поиска платной парковки в точке остановки.

    Usage: parking_detector <options...>

        --index-dir <dir>           Carparks index directory containing carparks.mms.1 and rtree.mms.1
        -L, --log-level LOG_LEVEL   Logging level (debug, info, warn,error, fatal)
        -l, --search-limit N        Parking search limit
        -r, --search-radius R       Parking search radius


Для скачивания геоданных парковок и запуска одной командой есть скрипт-обёртка
((https://a.yandex-team.ru/arc/trunk/arcadia/maps/automotive/parking/tools/qa/parking_detector.sh tools/qa/parking_detector.sh))

**Вход**

Точки остановки читаются со stdin в формате [YT JSON](https://yt.yandex-team.ru/docs/description/storage/formats.html#JSON)

* track_ref -  ID трека - источника точки
* lon - долгота точки остановки
* lat - широта точки остановки
* carpark_type - размеченный тип парковки (`free`, `toll`, `none`)
* carpark_org_id - ID организации парковки для `carpark_type=toll`, отсутствует для остальных типов

[Пример](samples/data/parking_points.ytjson) сохранненного YT JSON. Замечание: файл содержит дополнительные поля,
которые не используются детектором

**Выход**

Результат поиска выдаётся в stdout в виде [YT JSON](https://yt.yandex-team.ru/docs/description/storage/formats.html#JSON)

Для каждой точки со входа выдаётся один объект на выходе:

* track_ref - то же, что и на входе
* lon - то же, что и на входе
* lat - то же, что и на входе
* expected_carpark_org_id - carpark_org_id из входного объекта
* detected_carpark_org_id - ID организации парковки, если детектор определил платную парковку в точке остановки

[Пример](samples/data/detected_parking_points.ytjson) выхлопа

### Примеры использования

Отгружаем выхлоп в YT

    $> yt read-table --format json //home/maps/users/euag/parking_qa/parking_points \
       | ./tools/qa/parking_detector.sh \
       | yt write-table --format json //home/maps/users/euag/playground/detected_parking_points

Читаем табличку с размеченными точками парковки из YT, прогоняем через тестовый детектор парковок и
считаем метрики с помощью`stat_parking_detector`

    $> yt read-table  --format json //home/maps/users/euag/parking_qa/parking_points \
       | ./tools/qa/parking_detector.sh \
       | ./tools/qa/stat_parking_detector/stat_parking_detector


## Формат хранения трека

Формат - JSON, один объект на файл.

Свойства корневого объекта:

* `ref_id` - уникальный ID трека. Сейчас генерится как `imei`_`start_timestamp`
* `start_timestamp`/`end_timestamp` - время начала/конца трека.
* `parking_point` - точка остановки для тестирования
    * `parking_point.timestamp` - время остановки
    * `parking_point.position` - место остановки
    * `parking_point.parking_id` - (опционально) ID платной парковки, если она есть в месте остановки.
* `track.records` - список точек трека.
* `meta` - метаинформация, нужна для понимания откуда данные трека взяты.

# Точки трека в track.records

* `timestamp`
* `position`
    * `position.lon`, `position.lat` - GPS-координаты
    * `position.speed` - скорость по GPS
* `can` - данные CAN-шины, принятые в момент веремни.
    * `can.speed` - скорость
    * `can.events` - список событий


### Пример

    {
        "ref_id": "861108034383702_1567288243",
        "start_timestamp": 1567288243,
        "end_timestamp": 1567289993,
        "meta": {
            "imei": 861108034383702,
            "ride_index": 1,
            "ruler_url": "https://nda.ya.ru/3VnXjy",
            "source": "//home/maps/users/euag/tele-events-2019-09-01",
            "track_tail": 50
        },
        "parking_point": {
            "parking_id": "placeholder",
            "timestamp": 1567289993,
            "position": {
            "lon": 37.35502625,
            "lat": 55.64029312
            }
        },
        "track": {
            "records": [
                {
                    "timestamp": 1567289954,
                    "position": {
                    "lon": 37.35974121,
                    "lat": 55.64276505,
                    "speed": 56
                    },
                    "can": {
                    "events": [
                        "IGN_ON"
                    ]
                    }
                },
                {
                    "timestamp": 1567289954,
                    "position": {
                    "lon": 37.35974121,
                    "lat": 55.64276505,
                    "speed": 56
                    },
                    "can": {
                    "speed": 54
                    }
                },
            ...
            ]
        }
    }

## track_matcher

Инструмент был удалён в связи с задачей YCARBACKEND-648.
Если его когда-то понадобится использовать, придётся вернуться назад с помощью системы контроля версий.

Инструмент для матчинга списка GPS сигналов на граф.

    Usage: track_matcher <options...> files...

        -L, --log-level LOG_LEVEL   Logging level (debug, info, warn,error, fatal)
        -c, --config-file file      Matcher Config file
        -o, --output-dir dir        Output dir
        -k, --keep-unmatched        Keep unmatched signals
        -l, --last-signals <n>      Match last <n> signals


**Вход**

Данные графа для matcher: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/graph

Пути к полученным файлам можно задать в Matcher Config file:
    "graph_data", "graph_topology", "edges_rtree", "edges_persistent_index".

Формат - JSON

* `track.id` - уникальный ID трека.
* `track.records` - список точек трека.

# Точки трека в track.records

* `timestamp`
* `position`
    * `position.lon`, `position.lat` - GPS-координаты
    * `position.direction` - Направление двежения в градусах
    * `position.speed` - Скорость в м/с

### Пример

    {
        "track": {
            "id": "asdfs",
            "records": [
                {
                    "timestamp": 1567289954,
                    "position": {
                    "lon": 37.35974121,
                    "lat": 55.64276505,
                    "direction": 10,
                    "speed": 10
                    },
                },
                {
                    "timestamp": 1567289954,
                    "position": {
                    "lon": 37.35974121,
                    "lat": 55.64276505,
                    "direction": 11,
                    "speed": 10
                    },
                },
            ...
            ]
        }
    }


**Выход**

Результат записывается в Output dir

Формат - JSON

* `track.id` - уникальный ID трека.
* `track.records` - список точек трека.

# Точки трека в track.records

* `timestamp`
* `position`
    * `position.lon`, `position.lat` - GPS-координаты

### Пример

    {
        "track": {
            "id": "asdfs",
            "records": [
                {
                    "position": {
                    "lon": 37.35974121,
                    "lat": 55.64276505,
                    },
                },
                {
                    "position": {
                    "lon": 37.35974121,
                    "lat": 55.64276505,
                    },
                },
            ...
            ]
        }
    }
