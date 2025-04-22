Unshown Popular Organisations
===

Этот пайплайн был создан чтобы регуляризовать выдачу непоказов популярных организаций, которая была проанализирована [тут](https://a.yandex-team.ru/arc/trunk/arcadia/maps/geoq/experiments/check_poi_rendering). 

### Информация для потребителей

| Key | Value |
|---|---|
| Ответственные разработчики | Василий Варенов [(iambackend@)](https://staff.yandex-team.ru/iambackend) |
| Вопросы и пожелания | Дмитрий Корнев [(tswr@)](https://staff.yandex-team.ru/tswr) <br/> Василий Варенов [(iambackend@)](https://staff.yandex-team.ru/iambackend) |
| Исходники | [Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/unshown_popular_orgs) <br/> [Sandbox](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/geoq/GeoqUnshownPopularOrgs) |
| Шедулеры в Sandbox | [Подготовка данных](https://sandbox.yandex-team.ru/scheduler/696378/view) |
| Таблицы в YT | [top_unshown](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/unshown_popular_orgs/latest/top_unshown) <br/> [unshown_orgs](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/unshown_popular_orgs/latest/unshown_orgs) |

## Технические детали

В качестве исходных данных используется [renderer_impressions]((https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/renderer_impressions)), [features_schematized]((https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/personalized_poi/group/features_schematized)) и [static_poi/stable/latest]((https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/static_poi/stable/latest)). Из первой собирается информация о том, показывается ли организация на карте, из второй различная информация об организации, в том числе статистика по кликам и посещениям, из третьей берется диспкласс и информация о возможных причинах непоказа.

Берутся только организации, которые неотображаются на карте и отфильтровываются следующие случаи:
* Foreign организации
* Временно закрытые организации
* Геообъекты и жилые комплексы
* Военкоматы и прочие организации из [списка](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/static_poi/poi.py) организаций которые недолжны отображаться 
* Транспортные объекты, так как они неправильно учитываются в `renderer_impressions`
* Торговые центры, так как часто на дальних зумах они не показываются из-за метро или каких-то более приоритетных пайов, а на ближних зумах у них открывается индор. Это не очень похоже на проблему.


Потом из получившихся отбирается ~9000 организаций если они попадают в топ-1 персентиль (можно передать свои персентили) внутри города `city_id` по одному из параметров:
* disp_class
* deep_clicks_count__180_days
* orgvisits__180_days
`city_id` бывает равен нулю, это значит что город не был найден для данной организации и она считается вне города (селе), и для этой категории так же считается персентиль, как и для остальных городов.

## Зачем нужна папка yql_udf и как вообще запустить пайплайн (смотри [сюда](https://a.yandex-team.ru/arc/trunk/arcadia/maps/geoq/hypotheses/flats/README.md))

Запускать пайплайн надо так:
```sh
cd ~/arcadia/maps/poi/unshown_popular_orgs
ya make -r
# Prepare
NILE_YQL_PYTHON_UDF_PATH=./yql_udf/libunshown_popular_orgs-yql_udf.so  ./bin/unshown-popular-orgs --results-dir //path/to/yt/dir
```
