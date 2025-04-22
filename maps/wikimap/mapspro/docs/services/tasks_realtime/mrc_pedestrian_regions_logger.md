MRC Pedestrian Regions Logger
=============================
Процесс записывает события с зонами контроля заданий пешеходам в [таблицу на YT][yt table]. Эта таблица содержит следующую информацию:
- Название и идентификатор зоны.
- Статус зоны.
- Идентификатор компании-подрядчика.
- Признаки зоны: "В помещении", "Панорамная" и "Тестовая".
- Логин и идентификатор исполнителя.
- Идентификатор административной единицы привязанной к зоне.

Представляет собой pub-sub процесс обрабатывающий коммиты связанные с:
- объектами категории `mrc_pedestrian_region`; и
- связями `mrc_pedestrian_region_associated_with`.


Таблица
-------
MRC Pedestrian Regions Logger не создаёт таблицу автоматически, а лишь добавляет новые записи в существующую. Однако, эта таблица легко создаётся следующими двумя коммандами:

```
ya tool yt create --type table --recursive --proxy hahn \
--path //home/maps-nmaps/analytics/logs/mrc-pedestrian-region-log
```

```
ya tool yt alter-table --proxy hahn \
--path //home/maps-nmaps/analytics/logs/mrc-pedestrian-region-log \
--schema '[
  {name="timestamp";        type="timestamp"; required=%true};
  {name="object_id";        type="int64";     required=%true};
  {name="name";             type="string"};
  {name="company_id";       type="string"};
  {name="status";           type="string";    required=%true};
  {name="is_indoor";        type="boolean"};
  {name="is_panoramic";     type="boolean"};
  {name="is_testing";       type="boolean"};
  {name="pedestrian_uid";   type="int64"};
  {name="pedestrian_login"; type="string"};
  {name="ad_id";            type="int64"}
]'
```


[yt table]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/nmaps/analytics/logs/mrc-pedestrian-region-log
