### Мониторинг статистики по трафаретам
Основной код живет в [https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction_py/lib/trafaret_monitoring](библиотеке).

Конфиги задаются в формате json, имеется протобуфная схема. Есть возможность указывать ключи для разрезов из набора
```Day, PageID, ExperimentBits, IsAuctionStable, IsNav``` и дополнительные фильтры по ```TypeID, PageID```.
Можно использовать один из стандартных конфигов, либо использовать свой кастомный конфиг. Имеется набор
[https://a.yandex-team.ru/arc/trunk/arcadia/ads/quality/simulate_auction_py/lib/trafaret_monitoring/config](стандартных кофингов),
которые вкомпиливаются в либу в виде ресурсов.

Пример конфига
```
{
    "TypeID": 1,
    "Experiments": [
        {
            "ExperimentID": 297,
            "ExperimentBits": 3489660928
        }
    ],
    "PageID": [2],
    "Keys": ["IsAuctionStable", "IsNav"],
    "SrcTables": {
        "BasePath": "home/bs/logs/JoinedEFHFactors/1h"
    },
    "DstTables": {
        "BasePath": "home/bs/trafaret_monitoring/search/1d"
    },
    "SolomonConfig": {
        "GroupName": "search",
        "Fields": ["CtrFactor", "HitsRatio", "ShowsRatio"]
    }
}
```

Режим ```range_query``` - запуск расчета статистики по трафаретам за выбранный промежуток времени. Записывает результат в виде таблицы на YT и выдает на stdout в виде списка json-объектов для записи в файл.
```
./trafaret_monitoring --config [search|...] range_query --range YYYYMMDD..YYYYMMDD [--dry-run] > data.json

# --config - один из стандартных конфигов
# --config-file - путь до кастомного конфига, если задан, то имеет приоритет над --config
# --range - диапазон дат
# --dry-run - не запускать запрос, только распечать текст запроса
```

Режим ```push_to_solomon``` - загрузка данных из json-файла в мониторинг на Solomon.
```
./trafaret_monitoring --config [search|search-mobile|...] push-to-solomon --data-file FILE.JSON --timestamp YYYYMMDD

# --config или --config-file - конфигурация, включающая в себя настройки для загрузки в Solomon
# --data-file - файл с выхлопом режима range_query
# --timestamp - метка времени для Solomon
```

Режим ```regular``` - регулярный сбор статистики и загрузка на Solomon. В этом режиме сначала выполняется проверка наличия необходимых входных таблиц логов на заданную дату и проверка наличия выходных таблиц. Если входные таблицы есть, а выходных еще нет, то выполняется запрос и результат загружается на Solomon. С помощью этого режима мониторин можно зашедулить в крон или на сендбокс.
```
./trafaret_monitoring --config [search|...] regular [--date YYYYMMDD] [--max-days-ago N]

# --date - если не указана, то today() - дата запуска
# --max-days-ago - сколько дней назад от даты запуска обрабатывать
```
