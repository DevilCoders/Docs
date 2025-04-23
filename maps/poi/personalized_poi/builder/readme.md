## Конвеер подготовки данных для Personalized POI

Цель: в рамках регулярного процесса агрегировать пользовательские данные,
строить по ним персональные POI, раскладывать эти данные на бекенды.

## Регулярные процессы
* [Conveyor scheduler](https://sandbox.yandex-team.ru/scheduler/9930/view) — запускает регулярный процесс конвеера
* [Basemape dumper scheduler](https://sandbox.yandex-team.ru/scheduler/9908/view) — запускает регулярную выгрузку из подложки

## Ключевые компоненты

* [Sandbox conveyor](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/PersonalPoiGenerator/ConveyorV2) — 
  исходники конвеера, который запускается Conveyor scheduler
* [Extractor](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor) — 
  бинарник, используемый конвеером для выполнения большинства задач
* [Poi packer](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/poi_packer) —
  упаковывает подготовленные данные в fbs формат

## Мониторинги конвеера
* Распределения Personalized POI: [отчёты](https://stat.yandex-team.ru/Maps.Wiki/GEOQ/PersonalizedPOI/) в стат, [дашборд](https://datalens.yandex-team.ru/ry1prljyxrq0m-analitika-personalized-poi)
* [Ecstatic dataset](http://ecstatic.maps.yandex.net/pkg/yandex-maps-perspoi-renderer/versions)

## Стадии подготовки данных
* [Инициализация](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/init_folders.py) [директорий](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/personalized_poi) на hahn
* [Обновление](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/update_dict.py) соответствий permalink-oid, cid-puid,y uid-puid
* Извлечение информации из внешних источников
    * [Карточные логи](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/extract_from_maps_logs.py) из [таблиц](https://yt.yandex-team.ru/hahn/navigation?path=//home/geosearch/personal_features/group)
    * [Закладки](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/extract_from_bookmarks.py) из [таблиц](https://yt.yandex-team.ru/hahn/navigation?path=//home/datasync/fulldump/maps_common/ymapsbookmarks1/bookmarks)
    * [Посещения](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/extract_from_orgvisits.py) из [таблиц](https://yt.yandex-team.ru/hahn/navigation?path=//home/user_identification/orgvisits/prod/state/export)
    * [Подложка](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/extract_from_base_map.py) из [выгрузки](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/personalized_poi/tmp/base_map) [basemap dumper](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/PersonalPoiGenerator/PoisDumper)
    * [Common addresses (работа-дом)](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/extract_from_common_addresses.py) из [таблиц](https://yt.yandex-team.ru/hahn/navigation?path=//home/datasync/fulldump/profile/addresses/common_addresses)
    * [Regulargeo](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/extract_from_regulargeo.py) из [таблиц](https://yt.yandex-team.ru/hahn/navigation?path=//home/user_identification/usergeo/production/state/regulargeo-export)
    * [Координаты организаций в YmapsDF](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/extract_from_ymapsdf_positions.py) из [таблиц](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/ymapsdf)
* [Выгрузка данных Справочника](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/extract_from_altay.py) из [таблиц](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/snapshot)
* Добавление информации для опубликованных организаций Справочника
    * [Имя в YmapsDF](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/extract_from_ymapsdf.py) из [таблиц](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/ymapsdf)
    * [Причины непопадания на текущую версию подложки](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/basemap/poi_checker)
* [Объединение извлеченных данных](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/join.py)
* [Вычисление близких организаций](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/calculate_near_organisations.py)
* [Подготовка](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/prepare_features.py) таблицы [features](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/personalized_poi/group/features_schematized&offsetMode=row)
* [Расчет минимальных зумов](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/calculate_zoom.py)
* [Подготовка](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/fill_ecstatic_tables.py) [таблиц](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/personalized_poi/ecstatic) для Ecstatic
* [Загрузка в Ecstatic](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/PersonalPoiGenerator/UploadToEcstatic) при помощи [бинарника](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/poi_packer)
* [Расчет распределений](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/calculate_statistics.py)

## Ранжирование персональных POI
### Используемые фичи
* "puid" - идентификатор пользователя
* "oid" - идентификатор организации
* "base_zoom" - зум, на котором изначально распределялся POI
* "bookmarks" - лежит ли POI в закладках у пользователя
* "city_id" - идентификатор города, в котором находится организация
* "days_deep_clicks_count_*" - количество дипюзов за все время, за 365 дней, за 180 дней
* "days_good_clicks_count_*" - количество кликов за все время, за 365 дней, за 180 дней
* "home_distance" - расстояние до дома пользователя
* "is_geo_product" - является ли организация геопродуктовой
* "is_indoor" - попадает ли организация в схемы помещений
* "is_publish" - опубликован POI на карте или нет
* "is_temporarily_closed" - временно закрыт 
* "last_deep_click_day" - день, когда был последний дипюз
* "last_good_click_day" - день, когда был последний гудюз
* "lat" - широта
* "lon" - долгота
* "main_rubric" - основная рубрика
* "name" - текстовое название организации
* "name_is_sensitive" - чувствительность имени организации
* "orgvisits_*" - количество посещений за 180 дней, за 60 дней
* "regulargeo_accumulative_radiance" - удаленности от работы/дома
* "rubric" - рубрика
* "s_orgvisit_seconds_*" - количество секунд, проведенных в организации за 180 дней, за 60 дней
* "stat_deep_clicks_count" - количество дипюзов по всем пользователям за 700 дней
* "stat_deep_clicks_count" - количество гудюзов по всем пользователям за 700 дней
* "work_distance" - расстояние до работы пользователя

### Формула
Используется [formula10](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/pylibs/ranking/formulas.py)
