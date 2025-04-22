# export_poi_worker

Генератор фида для Справочника

# Источник данных

### База сервиса "Народная карта"
Данные считываются из базы НК инструментом [json2ymapsdf](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/tools/ymapsdf-conversion/json2ymapsdf)
Инструмент конвертирует данные в формат [ymapsdf](https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/ymapsdf)
Используюя специальные настройки и правила преобразования описанные тут [export_poi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/tools/ymapsdf-conversion/json2ymapsdf/cfg/export_poi)
### Таблица sprav.merge_poi_altay_feed_unknown
Данные из таблицы nyak_mapping_unknown считанные merge_poi_worker

# Объекты экспорта
Экспортируются объекты из ymapsdf базы принадлежащие ft_type, для которых определено соответствие с рубрикой Справочника
[rubrics_mapping.xml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/cfg/rubrics/rubrics_mapping.xml)

Не все объекты являются POI в терминологии НК. В фид также отгружаются центроиды растительности, остановки транспорта и т.п.

# Результат экспорта
Результатом экспорта является набор .xml файлов в .gz с контрольными суммами на mds
http://storage-int.mds.yandex.net:80/get-mpro-dataset/
последний результат доступен справочнику тут:
http://core-nmaps-dataset-explorer.maps.yandex.net/v0.1/export-latest/poi/[имя файла]

## Файлы основного фида
| Файл| Описание |
|---|---|
|poi_export_accurate_rubric_id.xml.gz|Файл объектов НК для которых проставлена рубрика. Это всегда POI|
|poi_export_calculated_rubric_id.xml.gz|Файл объектов в НК которые не имеют рубрики и она проставлена в соответствии с таблицей rubrics_mapping.xml|
|poi_export_indoor_feed.xml.gz|Файл POI из схем помещений.|
|poi_export_entrances.yson.gz|Файл со входами в организации из НК.|

#### Пример фрагмента фида с POI:
```XML
<company>
  <company-id>3412227748</company-id>
  <disp_class>9</disp_class>
  <name lang="en">Raiffeisenbank</name>
  <name lang="ru">Райффайзенбанк</name>
  <shortname lang="ru">Райффайзенбанк</shortname>
  <coordinates>
    <lon>37.665952</lon>
    <lat>55.785421</lat>
  </coordinates>
  <rubric-id>184105402</rubric-id>
  <actualization-date>1571966106928</actualization-date>
  <modified-by>685892448</modified-by>
  <permalink>1262236890</permalink>
  <!--Поле есть только в POI из схем помещений - внутренний идентификатор уровня схемы-->
  <indoor-level-universal>3</indoor-level-universal>
</company>
```
(На самом деле основной фид содержит больше полей, но они не актуальны и будут удалены)

#### Пример фрагмента фида со входами:
```JSON
[
    {
        "originalId": "123",
        "permalink": 1262236890,
        "entrances": [
            { "lon": 37.665953, "lat": 55.785422, "type": "other" },
            { "lon": 37.665954, "lat": 55.785423, "type": "other" }
        ]
    },
    {
        "originalId": "456",
        "permalink": 1262236891,
        "entrances": []
    }
]
```

Пустой вектор входов означает, что все входы были сознательно удалены в Народной карте.

## Файлы дополнительного фида
Или файлы пользовательского состояния.
В этот фид попадают объекты POI для которых включена синхронизация (процесс применяющий данные Справочника к POI НК).
Те ft_type которых перечислены тут:
[business_merged_ft_type_ids.xml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/cfg/editor/business_merged_ft_type_ids.xml)

Это делается для того, чтобы можно было отличить состояния объектов по мнению Справочника, от состояния определённого пользователями НК.
И Справочник не "обелял" своё представление получая его же из фида.

| Файл| Описание |
|---|---|
|poi_export_coords_feed.xml.gz|Файл с координатами POI, которые последний раз устанавливал пользователь НК, а не Справочник|
|poi_export_names_feed.xml.gz|Файл с именами POI, которые последний раз устанавливал пользователь НК, а не Справочник|
|poi_export_indoor_names_feed.xml.gz|Файл с именами indoor POI, которые последний раз устанавливал пользователь НК, а не Справочник.|
|poi_export_verified_coords_feed.xml.gz|Файл с данными POI для которых в Народной Карте выставлено соответствие или точность координат|

Для координат POI indoor не генерируется фид пользовательских координат, т к Справочник не может модифицировать координаты в схеме помещений,
и основной фид их содержит.

#### Пример фрагмента фида с координатами:
```XML
<company>
  <company-id>1520813408</company-id>
  <coordinates>
    <lon>36.225300</lon>
    <lat>50.002700</lat>
  </coordinates>
  <publishing-status>publish</publishing-status>
  <permalink>1049457248</permalink>
  <rubric-id>184106344</rubric-id>
  <actualization-date>1424108780892</actualization-date>
</company>
```
#### Пример фрагмента фида с именами:
```XML
<company>
  <company-id>3412227748</company-id>
  <name lang="ru">Райффайзенбанк, банкомат</name>
  <shortname lang="ru">Райффайзенбанк</shortname>
  <rubric-id>184105402</rubric-id>
  <actualization-date>1571966106928</actualization-date>
  <permalink>1262236890</permalink>
  <indoor-level-universal>3</indoor-level-universal>
</company>
```

# Процесс работы
Процесс экспорта запускается по [расписанию](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/services/tasks_sprav/docker/install/etc/template_generator/templates/etc/cron.d/wiki-export-poi-worker)

Этапы:
1. Определяется номер "релизной ветки" НК - тот snapshot данных НК который будет опубликован в ближайшее время.
2. При помощи json2ymapsdf создаётся postgresql база с ymapsdf представлением snapshot
3. Загружается список объектов из таблицы ft
4. Для загруженных объектов проверяется наличие permalink - связи с объектом Справочника.
   Если его нет то проверяется nyak_mapping_unknown и берётся пермалинк из него, а если и там нет
   и объект из списка ft_type двустороннего фида ему назначается специальный зарезервированный permalink (см далее)
5. Для объектов обновляется информация о последнем пользовательском состоянии.
6. Данные каждого объекта записываются в соответствующие файлы.
7. Все текущие состояния объектов записываются в БД Народной карты для последующего обратного фида. (sprav.export_poi_worker_feed_data)
8. Формируются фаылы и помещаются в mds

# Зарезервированные permalink
Если объекту не назначен permalink пользователем, предпологаем, что он не нашёл в подсказке нужной организации.
Для того, чтобы сигнализировать Справочнику о необходимости создать новую карточку, мы искуственно резервируем permalink из набора в 10 миллионов
выданных заранее, которые сам Справочник, не использует.

# Кэш пользовательских состояний
Это таблица в БД НК sprav.export_poi_worker_component_feed_cache
При каждом обращении к функции получения данных из кэша, сравнивается текущая ревизия объекта и та, что в кэш.
Если есть обновление, кэш освежается поиском действий пользователя между этими ревизиями.
Пока кэш не очищается при удалении объектов.
