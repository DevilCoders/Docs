### Что это

travel/avia/shared_flights/tasks/regular_flights - это скрипт, отвечающий за выгрузку данных из базы расписаний Авиарейсов в yt
за заданный период времени (обычно за 13 или 26 недель).
Используется в sandbox задаче: https://a.yandex-team.ru/arc_vcs/sandbox/projects/avia/travel_avia_dump_resource/task/__init__.py

На данный момент для того чтобы обновить дамперы, используемые в TravelAviaDumpRegularFlights нужно выполнить команду:
```(sh)
ya package --upload --sandbox --upload-resource-type=TRAVEL_AVIA_DUMP_REGULAR_FLIGHTS_BINARY --upload-resource-attr=resource_name=regular_flights regular_flights/pkg.json
```


### Пример запуска из командной строки:

cd regular_flights
./regular_flights --AVIA_YQL_TOKEN={token} --AVIA_RF_OUTPUT_YT_TABLE=//home/avia/dev/u-jeen/regular-flights --AVIA_RF_START_DATE=-4 --AVIA_RF_END_DATE=-2


Замечание. Надо бы поменять вот эту строчку кода 
https://a.yandex-team.ru/arc/trunk/arcadia/travel/avia/shared_flights/tasks/regular_flights/internal/regular_flights.go?rev=r9568641#L347
на yt.WriteTable(). Как сейчас написано, у робота не получается создать новую таблицу, но получается перезаписать старую.
Для быстрой отладки можно копировать 1-week таблицу из https://yt.yandex-team.ru/hahn/navigation?path=//home/avia/dev/u-jeen/regular-flights в нужный путь.
