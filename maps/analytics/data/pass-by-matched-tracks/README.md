## Скрипт для расчета заездов или проездов
Здесь хранится скрипт, которые по списку полигонов может считать зазеды пользователей в эти полигоны и проезды пользователей около них


## Пример запуска

Запускаем файл [pass-by-matched-tracks/ya.make](/arc/trunk/arcadia/maps/analytics/data/pass-by-matched-tracks/ya.make). Входной параметр - таблица с полигонами объектов, для которых хотим посчитать заезды. Пример строчки с параметрами:
```angular2html
-d 20210701_ --daily -c polygon -s uuids --clids navi ymaps taxi
-i //home/zapravki/production/snippet_stations --name-field StationId
-o //home/zapravki/production/stations_stat/visits_uuids/ --mark out

```
