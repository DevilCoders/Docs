===Что это

travel/avia/shared_flights/api/cmd/dumper - это приложение, отвечающее за выгрузку данных из базы расписаний Авиарейсов в pb2 файлы.
Используется в sandbox задаче: https://a.yandex-team.ru/arc_vcs/sandbox/projects/avia/travel_avia_dump_resource/task/__init__.py

На данный момент для того чтобы обновить дамперы, используемые в TravelAviaDumpResource нужно выполнить команду:
```(sh)
ya package --upload --sandbox --upload-resource-type=TRAVEL_AVIA_DUMP_RESOURCE_BINARY --upload-resource-attr=resource_name=dumper dumper/pkg.json
```
