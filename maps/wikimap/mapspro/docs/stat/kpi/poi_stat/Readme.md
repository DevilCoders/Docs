# Статистика POI в Народной карте

Скрипт выполняет расчёт метрик POI в Народной карте в сравнении с Яндекс.Бизнесом.

## Дашборд

Дашборд в [DataLens](https://datalens.yandex-team.ru/cpz3brv2802m5-poi-nk-vs-yandeks-biznes).

На любой вкладке есть селекторы региона геобазы, интересующей группы POI и даты. Вся остальная информация будет показана с учётом этих фильтров.

Вкладки:
* **Статистика** - агрегированные метрики (детально см. ниже в п. 2 раздела "Результаты")
* **Расхождение по расстоянию** - список POI в порядке убывания расстояния между координатами в НК и Алтае
* **Дубли пермалинков (Алтай)** - список POI, пермалинки которых различаются в `alpha`-стадии YMapsDF и Алтае
* **Дубли пермалинков (YMapsDF)** - список POI, пермалинки которых различаются в `alpha` и `final`-стадиях YMapsDF
* **Без пермалинков** - список POI, для которых отсутствует пермалинк в Алтае
* **Закрыть в НК** - список POI, для которых есть пермалинк в Алтае, но он помечен как "точно закрыта"

## Исходные данные

Исходными данными являются:
* `alpha`-стадии последних поставок каждого региона публикации [YMapsDF](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf)
* `final`-стадии последних поставок каждого региона публикации YMapsDF
* [nyak-mapping](https://yt.yandex-team.ru/hahn/navigation?path=//home/altay/db/export/current-state/snapshot/nyak_mapping)

Для каждого региона публикации поставка определяется отдельно и независимо от других. Опираться на [latest YMapsDF](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest) не получится - эта ссылка всегда указывает на `final`-стадию одного датасета, содержащего на момент экспорта **сразу все** регионы публикации. Если после этого экспорт из Народной карты достаточное время приезжал частями (не по всем регионам сразу), то `alpha`-стадия, соответствующая `latest`, может быть уже недоступна из-за давности.

Статистика считается по [дереву регионов геобазы](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/geo-data/major_regions_map).

## Результаты

Расчёты производятся в два этапа:
1. Строится таблица [raw](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/poi-stat/raw) с "сырыми" данными по POI по данным из YMapsDF и Яндекс.Бизнеса:
 * `ft_id`
 * `ft_type_id`
 * `p_ft_id`
 * `p_ft_type_id`
 * `permalink_id` (пермалинк Яндекс.Бизнеса из `nyak-mapping`)
 * `permalink_id_ymapsdf` (пермалинк из `final`-стадии YMapsDF)
 * `geom_nk`
 * `geom_altay`
 * `region_id` (из геобазы, рассчитывается по geom_nk)
 * `dist` (расстояние между `geom_nk` и `geom_altay` в метрах)
 * `position_quality`
 * `is_closed` (для точно закрытых организаций)

2. По этим данным строятся остальные таблицы, используемые непосредственно в дашборде:
* [metrics](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/poi-stat/metrics) - агрегированные метрики
 * `total_count` - всего
 * `verified_count` - верифицированных
 * `to_close` - закрыть в Народной карте
 * `no_permalink` - нет пермалинка
 * `ambiguous_permalinks` - неуникальных пермалинков (1 пермалинк - несколько объектов НК) по данным из Яндекс.Бизнеса
 * `ambiguous_ft_ids` - объектов НК с неуникальными пермалинками по данным из Яндекс.Бизнеса
 * `ambiguous_permalinks_ymapsdf` - неуникальных пермалинков (1 пермалинк - несколько объектов НК) по данным из YMapsDF
 * `ambiguous_ft_ids_ymapsdf` - объектов НК с неуникальными пермалинками по данным из YMapsDF
 * `dist_equal` - объектов с совпадающими координатами (расхождение не больше 0.5 м)
 * `dist_over_Xm` - смещено более, чем на X м (0.5, 5, 10, 20, 50, 100, 500)
 * `pos_quality_X` - объектов с заданным значением точности координат
* [dist](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/poi-stat/dist) - таблица POI с расхождением
* [close](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/poi-stat/close) - таблица POI к закрытию в Народной карте
* [no-permalink](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/poi-stat/no-permalink) - таблица POI без пермалинка
* [ambiguous-permalinks](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/poi-stat/ambiguous-permalinks) - таблица POI с неуникальными пермалинками по данным из Яндекс.Бизнеса
* [ambiguous-permalinks-ymapsdf](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/poi-stat/ambiguous-permalinks-ymapsdf) - таблица POI с неуникальными пермалинками по данным из YMapsDF

**Примечание**: метрики `dist_equal` и `dist_over_Xm` вычисляются только для тех POI, у которых есть и координаты НК, и координаты Яндекс.Бизнеса. А у POI, попавших в группы `to_close` и `no_permalink`, координаты из Яндекс.Бизнеса отсутствуют. Поэтому метрики за конкретную дату связаны соотношением:

`total_count = dist_equal + dist_over_half_m + to_close + no_permalink`

Все таблицы для дашборда рассчитываются с разбивкой по группам POI:
* все
* защищённые (`ft_type_id` из защищённого [списка](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/ymapsdf/lib/merge_poi/data/merge_poi.json))
* незащищённые
* верифицированные (установлено хотя бы одно соответствие и/или точность "точно"/"приблизительно")
* схемы помещений (родительским объектом является уровень схемы помещений с `ft_type_id`=2302)

## Автоматический запуск

* [Nirvana Graph](https://nirvana.yandex-team.ru/flow/40705809-6623-4dfe-84fd-2769a9a8915d)
* [Reactor](https://nirvana.yandex-team.ru/browse?selected=9979454)

## Ручной запуск

Команда для запуска:
```
YT_TOKEN=<robot-wikimap-yt-token> YQL_TOKEN=<robot-wikimap-yql-token>
ya nile ./bin/libpoi_stat.so run -- --proxy 'hahn' --use-yql
--result-path '//home/maps/core/nmaps/analytics/poi-stat' --scale 'daily' --dates 1970-01-01
```

Токены робота находятся в [секретнице](https://yav.yandex-team.ru/secret/sec-01cpqs004vh9nxcv6p26zk4k9b/).

Параметр `--use-yql` включает использование `yql`-бэкенда, для которого нужно собирать именно `UDF`.

Значения параметров `--scale` и `--dates` не имеют значения. Они являются обязательными из-за `statinfra_job`.

## Пересчёт метрик за конкретную дату

Модуль поддерживает пересчёт метрик из "сырых" данных за заданную дату. Для этого должна существовать таблица `$(result-path)/raw/YYYY-MM-DD` с соответствующими данными. Остальные таблицы будут перезаписаны со вновь вычисленными метриками.

Режим пересчёта включается опцией `--recalculate`, при этом параметр `--dates` обретает смысл и должен содержать дату для пересчёта.

Команда для запуска пересчёта:
```
YT_TOKEN=<robot-wikimap-yt-token> YQL_TOKEN=<robot-wikimap-yql-token>
ya nile ./bin/libpoi_stat.so run -- --proxy 'hahn' --use-yql
--result-path '//home/maps/core/nmaps/analytics/poi-stat' --scale 'daily' --dates 2021-01-01 --recalculate
```
