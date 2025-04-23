Библиотека для поиска новых зданий в местах обхода пешеходами
===

## Общая информация

При обходе приоритетных зон пешеходами требуется не только актуализировать 
известные Справочнику организации, но и по возможности находить новые. 
Неизвестные организации зачастую появляются в домах, которые недавно появились 
в этих зонах (были достроены, добавлены вручную или была получена недостающая 
информация).

Данная библиотека включает пайплайн и шедулеры, запускающие регулярный процесс 
поиска таких новых зданий в пешеходных зонах, а также собирающие информацию об 
уже известных организациях в этих зданиях.

### Информация для потребителей

| Что? | Где? |
|---|---|
| ABC | [maps-core-sprav-pedestrian](https://abc.yandex-team.ru/services/maps-core-sprav-pedestrian) |
| Экспорт в YT | [new_buildings](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/pedestrians/new_buildings) |
| Sandbox-шедулер | Sedem-managed [PEDESTRIANS_NEW_BUILDINGS](https://sandbox.yandex-team.ru/scheduler/703488/view) |
| Исходный код | [Пайплайн](https://a.yandex-team.ru/arc/trunk/arcadia/maps/sprav/pedestrians/new_buildings/bin) <br/> [Sandbox](https://a.yandex-team.ru/arc/trunk/arcadia/maps/sprav/pedestrians/new_buildings/task) |

## Технические детали

### Источники данных

Для консистентности с другими сервисами пешеходов актуальная информация о 
зданиях берется из таблиц Справочника, полученных в результате обработки 
экспорта Огорода:
- [bld](https://yt.yandex-team.ru/hahn/navigation?path=//home/altay/maps/current-state/bld) 
содержит атрибуты зданий.
- [bld_addr_txt](https://yt.yandex-team.ru/hahn/navigation?path=//home/altay/maps/current-state/bld_addr_txt) 
содержит человекочитаемые адреса зданий.
- [bld_geom](https://yt.yandex-team.ru/hahn/navigation?path=//home/altay/maps/current-state/bld_geom) 
содержит геометрию зданий.

Новые здания находятся путем сравнения текущего экспорта зданий с одним из 
архивных (которому не менее 30 дней). Месячные архивы доступны в 
[истории](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/ymapsdf_archive) 
ymapsdf-релизов.

Также используются следующие источники данных:
- [Полигоны обхода](https://yt.yandex-team.ru/hahn/navigation?path=//home/offline_data/walkers/pentagon/polygons_geometry)
- [Организации Справочника](https://yt.yandex-team.ru/hahn/navigation?path=//home/altay/db/export/current-state/snapshot/company)

### Как пользоваться

#### Ресурсы

В пайплайне используется nile-over-yql, который формирует YQL-операции с 
использованием специальным образом скомпилированного python-кода - yql udf. 
Поэтому утилита содержит два собираемых ресурса:
- [new_buildings](https://a.yandex-team.ru/arc/trunk/arcadia/maps/sprav/pedestrians/new_buildings/bin/new_buildings) - 
основной исполняемый бинарник.
- [libnew_buildings-yql_udf.so](https://a.yandex-team.ru/arc/trunk/arcadia/maps/sprav/pedestrians/new_buildings/yql_udf/libnew_buildings-yql_udf.so) - 
собранный из либы yql_udf ресурс, путь до которого добавляется в специальную 
переменную окружения `NILE_YQL_PYTHON_UDF_PATH`, после чего этот ресурс 
используется на YQL-бэкенде.

#### Пример запуска

```sh
cd ~/arcadia/maps/sprav/pedestrians/new_buildings
ya make -r
NILE_YQL_PYTHON_UDF_PATH=./yql_udf/libnew_buildings-yql_udf.so ./bin/new_buildings --output-table //home/maps/users/olegvp/new_buildings
```

Аргументы командной строки:
- `--date` - дата добавления зданий в формате `%Y-%m-%d`, если не задана - 
берется текущий день
- `--pool` - YT-пул, в котором запускаются map-reduce операции.
- `--output-table` - выходная таблица.

#### Выходные данные

Итоговая таблица содержит следующие поля:
- `bld_id` - уникальный идентификатор здания.
- `addresses` - человекочитаемый список адресов здания.
- `center` - центр полигона здания.
- `date` - дата добавления здания в качестве "нового".
- `organizations` - список известных организаций Справочника в здании (пермалинк 
и статус публикации у каждой).
- `orgs_count` - число организаций из поля выше.
- `polygon_ids` - список идентификаторов полигонов обхода.
- `shape` - геометрия здания в WKT-формате.
