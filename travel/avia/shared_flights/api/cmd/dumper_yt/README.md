===Что это

travel/avia/shared_flights/api/cmd/dumper_yt - это приложение, отвечающее за выгрузку данных из базы расписаний Авиарейсов в yt
за заданный период времени (обычно за вчерашний день; период не может простираться больше, чем на месяц в прошлое).
Используется в sandbox задаче: https://a.yandex-team.ru/arc_vcs/sandbox/projects/avia/travel_avia_dump_resource/task/__init__.py

На данный момент для того чтобы обновить дамперы, используемые в TravelAviaDumpYt нужно выполнить команду:
```(sh)
ya package --upload --sandbox --upload-resource-type=TRAVEL_AVIA_DUMP_YT_BINARY --upload-resource-attr=resource_name=dumper-yt dumper_yt/pkg.json
```
