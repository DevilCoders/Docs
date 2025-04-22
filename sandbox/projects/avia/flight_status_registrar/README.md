# Flight Status Registrars

Задачи для закупки статусов.

## Разработка

Подробнее про бинарные таски: https://wiki.yandex-team.ru/avia/dev/sandbox/

Далее на примере `OagFlightStatusRegistrar`

Внести правки в код бинарной таски `travel/avia/flight_status_registrar/oag`

Запустить тесты:
```
$ ya make --yt-store --checkout -t travel/avia/flight_status_registrar/oag
```

Проверить работу:
```
$ travel/avia/flight_status_registrar/oag/bin/oag_registrar
```

Собрать бинарную таску:
```
$ ya make --yt-store --checkout sandbox/projects/avia/flight_status_registrar/OagFlightsRegistrar
```

Загрузить бинарную таску:
```
$ ./sandbox/projects/avia/flight_status_registrar/OagFlightsRegistrar/OagFlightsRegistrar run --create-only --type AVIA_OAG_FLIGHTS_REGISTRAR --attr task_type=AVIA_OAG_FLIGHTS_REGISTRAR
```

В выводе ищем строчку `Uploading task #... created: https://sandbox.yandex-team.ru/task/...`, переходим по ссылки и релизим ресурс.
