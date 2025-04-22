# Пайплайн `generate_feeds`

Пайплайн генерирует пешеходные фиды для Справочника. Каждый день берётся
выгрузка данных пешеходов, и формируются все фиды с нуля начиная с 2018 года
(с этого года начинается отгрузка пешеходной информации). После этого строится
статистика о количестве полученных сигналов в определенных день из разных фидов.

Больше документации про справочник [тут](https://docs.yandex-team.ru/sprav/).

## Важные ссылки

| Что? | Где? |
| --- | --- |
| ABC | [maps-core-sprav-pedestrian](https://abc.yandex-team.ru/services/maps-core-sprav-pedestrian) |
| Графики | [datalens](https://datalens.yandex-team.ru/kbxiykpqqnaqd-pedestrians-metrics) |
| YT | Тестовые фиды: [//home/maps/poi/pedestrians/feeds](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/pedestrians/feeds)<br> Статистика фидов: [//home/maps/poi/statistics/pedestrians/feeds](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/pedestrians/feeds) <br> Продовый фид: [//home/altay/providers/tables/pedestrian](https://yt.yandex-team.ru/hahn/navigation?path=//home/altay/providers/tables/pedestrian) <br> Экспорт пешеходов: [//home/sprav/assay/tasker/walkers/export](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/assay/tasker/walkers/export) <br> Экспорт site_pedestrians: [//home/sprav/assay/common/site_pedestrian/export](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/assay/common/site_pedestrian/export) <br> Точность пешеходов: [//home/sprav/assay/tasker/walkers/tasks_with_precision](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/assay/tasker/walkers/tasks_with_precision) <br> Задачи в таскере: [//home/sprav/assay/tasker/TaskByProjects/MOBILE_TOLOKA_PEDESTRIAN](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/assay/tasker/TaskByProjects/MOBILE_TOLOKA_PEDESTRIAN) |
| Sandbox (текущий production) | Sedem-managed [Testing PEDESTRIANS_GENERATE_FEEDS](https://sandbox.yandex-team.ru/scheduler/700277/view) <br> Sedem-managed [Stable PEDESTRIANS_GENERATE_FEEDS](https://sandbox.yandex-team.ru/scheduler/700280/view) |
| Исходный код | Генерация фидов: [arcadia/sprav/altay/tools/pedestrian](https://a.yandex-team.ru/arc/trunk/arcadia/sprav/altay/tools/pedestrian) <br> Sandbox таска: [arcadia/maps/sprav/pedestrians/generate_feeds/task](https://a.yandex-team.ru/arc/trunk/arcadia/maps/sprav/pedestrians/generate_feeds) <br> Статистика: [arcadia/maps/sprav/pedestrians/generate_feeds/statistics](https://a.yandex-team.ru/arc/trunk/arcadia/maps/sprav/pedestrians/generate_feeds/statistics) <br> Запуск в cm: [arcadia/sprav/misc/cm/scripts/sunduk/graph.sh](https://a.yandex-team.ru/arc/trunk/arcadia/sprav/misc/cm/scripts/sunduk/graph.sh?rev=r8968798#L74) |

## Список фидов
1. `actualization` - организации, которые были актуализированны
2. `closing` - закрытые организации
3. `duplicates` - найденный дубликаты
4. `garbage` - сюда попадает все, что не попало в другие фиды (например, если
пешеход не смог зайти в организацию по внешним причинам, то информация об этом
попадёт сюда)
5. `last_bin_closing` - сюда попадают закрытие самых непопулярных организаций,
которые составляют 90% всех организаций
6. `site_pedestrian` - информация об организациях, которая была получена путем
промотра сайтов (было очень актуально во время карантина)
7. `sure_closing` - организации, которые были закрыты с большой степенью
уверенности
8. `temporal_closing` - временно закрытые организации
