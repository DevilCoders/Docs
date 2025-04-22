# Датасеты

## Календарь
Календарь праздничных дней. Не является, строго говоря, ОТ-сущностью, но активно используется.

https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/libs/calendar

Позволяет определять т.н. "тип дня". Тип дня – обобщение номера дня, используемое для учета праздников. Подробнее см. по ссылке выше и [в коде](https://a.yandex-team.ru/arc_vcs/maps/analyzer/libs/calendar/include/calendar.h?rev=c415b4ffcff3aca116bddc148cab09d845eb3406#L25).

Данные на YT: [//home/maps/jams/production/data/calendar/](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/data/calendar/)

Данные в ecstatic: [yandex-maps-calendar](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-calendar/versions)

## Статистические данные
Статистики скоростей на отдельных ребрах графа ОТ. Представлены несколько статистик (среднее, медиана и пр.) для множества временных отрезков (15-минуток или крупнее) различных типов дней (см. выше).

https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/libs/jams_statistical_data_4
(дока, в основном, ссылается на использование единой структуры в задаче предсказания ETA, но для ОТ использование аналогично)

Получаются обработкой [таблиц с подневными статистиками скоростей проездов](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/speed_statistics)

Данные на YT: [//home/maps/jams/production/masstransit/statistical_data](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/statistical_data)

Данные в ecstatic: [yandex-maps-masstransit-statistical-data](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-masstransit-statistical-data/versions)

## Модели
Обученные catboost-модели с [конфигами](configs.md).

Данные на YT: [//home/maps/jams/production/masstransit/models](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/masstransit/models)

Данные в ecstatic: [yandex-maps-masstransit-model](http://core-ecstatic-coordinator.maps.yandex.net/pkg/yandex-maps-masstransit-model/versions)
