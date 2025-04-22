Тут список ниток, к которым не надо подклеивать расписания мосгортранса. Подробнее про расписания МГТ на вики: https://wiki.yandex-team.ru/maps/dev/core/masstransit/data/MGT/

В файле надо писать id ниток, по одному в строке, без комментариев. Например:
```
153B_5_bus_rcabrest
3287659467
10274A_10t_minibus_rcagrodno
```

Список автоматически заливается в огород при каждом коммите задачей [MAPS_MASSTRANSIT_UPLOAD_MGT_BLACKLIST](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit/MapsMasstransitUploadMgtBlacklist). Задачу, конечно же, можно и вручную запустить.