Показы защищённых геопродуктовых POI 
===

## Общая информация

Проект предназначен для выяснения факта показа и количества показов геопродукта
на различных зумах. Доверять какому-то одному источнику не хочется, поэтому
используются три источника данных по показам: конфликты в народных картах,
показы в BEBR логах и тайлы рендерера. По ним получаем три таблицы impressions,
которые представляют собой список геопродукта (колонка `permalink`) с колонками
`impressions_10`, ..., `impressions_21`. В каждой колонке будет количество
показов POI (для `bebr`) или же сам факт показа/непоказа `1`/`0` (для `nmaps`
и `renderer`) на конкретном зуме. Эту информацию можно использовать для 
кросс-валидации, поиска миганий/дырок в показах и другой аналитики.

### Информация для потребителей
| Key | Value |
| --- | --- |
| Мейнтейнеры | [Maps.GeoQuality](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) |
| Шедулер в Sandbox | [Sheduler](https://sandbox.yandex-team.ru/scheduler/42872/view) |
| ABC сервис | [POI impressions checker](https://abc.yandex-team.ru/services/maps-core-poi-impressions-checker/) |
| Исходники | [Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/statistics/protected_geo_product/impressions) <br/> [Sandbox](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/maps/MapsCalcProtectedGeoproductImpressions/__init__.py) |
| Таблицы на YT | [impressions](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/protected_geo_product/impressions) |
| Графики | [dashboard](https://datalens.yandex-team.ru/kalqabqb04ikg-poi-metrics?tab=Epy) |

## Технические детали

### Collect geoproduct info
| Key | Value |
| --- | --- |
| Источники данных | [nyak mapping table](https://yt.yandex-team.ru/hahn/navigation?path=//home/altay/db/export/current-state/snapshot/nyak_mapping)
| | [Организации в алтае](//home/altay/db/export/current-state/snapshot/company) |
| | [Таблица static_poi](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/static_poi/stable/latest) |
| | [Весь геопродукт](https://yt.yandex-team.ru/hahn/navigation?path=//home/geoadv/export/production/priority_company_permanent_id) |
| | [ymapsdf](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/lates) |
| Результат | В папке на [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/protected_geo_product/impressions/geoproduct_info) |

Бинарь `collect_geoproduct_info` собирает всю необходимую информацию
о защищенном геопродукте из разных таблиц в одну для последующей обработки и
аналитики.
Поля итоговой таблицы:
 - `date` - дата сбора информации, нужны для джойна с другими таблицами в CHYT
 - `permalink` - пермалинк организации (из экспорта геопродукта)
 - `from_nmaps` - есть ли эта организация в Народной карте
(из `nyak_mapping_table`)
 - `found_in_ymapsdf` - есть ли эта организация в ymapsdf (из `ymapsdf`)
 - `ft_id` - `ft_id` организации (из `ymapsdf`). У одной организации может
быть больше одного `ft_id`, т.е. несколько меток на карте в разных местах.
 - `lat` - широта метки организации (из `ymapsdf`)
 - `lon` - долгота метки организации (из `ymapsdf`)
 - `disp_class` - `disp_class` метки организации (из `ymapsdf`)
 - `indoor_level_id` - есть ли у этой точки ссылка на схему индора. Если
ссылка не `NULL`, то значит эта точка находится в `indoor` (по `ymapsdf`)
 - `is_online` - является ли эта организация онлайн-организацией (из Алтая)
 - `is_exported` - экспортируется ли эта организация (из Алтая)
 - `type` - тип организации (из Алтая)
 - `publishing_status` - статус публикации организации (из Алтая)
 - `reasons_org_is_not_valid` - причины, по которым организация может не быть
 валидной (из `static_poi`)
 - `is_protected` - является ли организация защищенной (из `static_poi`).
Организация может быть не защищена в `static_poi` если была защищена совсем
недавно, и до `static_poi` эти изменения еще не дошли.
 - `is_recently_protected` - является ли организация недавно защищенной
(из `static_poi`)

### Bebr логи
| Key | Value |
| --- | --- |
| Источники данных | [org_statistics](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/data/org_statistics) |
| | [Выгрузка геопродукта](https://yt.yandex-team.ru/hahn/navigation?path=//home/geoadv/export/production/priority_company_permanent_id) |
| Результат | [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/protected_geo_product/impressions/bebr) |

В таблице `org_statistics` содержится статистика показов и кликов для каждой
организации по зумам. Выбрав из нее геопродукт и получаем таблицу
`impressions`.
Поля таблицы:
 - `permalink` - пермалинк организации
 - `impressions_N` - сколько раз организация была показана на N-ом зуме,
зумы с 10 до 21.

### Nmaps
| Key | Value |
| --- | --- |
| Источник данных | Редактор Народных карт http://core-nmaps-editor.maps.yandex.net |
| | [Подготовленные данные о геопродукте на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/protected_geo_product/impressions/geoproduct_info) |
| Результат | [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/protected_geo_product/impressions/nmaps) |

Информацию с народных карт запрашиваем с помощью [библиотеки](https://a.yandex-team.ru/arc/trunk/arcadia/maps/wikimap/mapspro/libs/editor_client).
Для каждого `ft_id` из `geoproduct_info` мы узнаем минимальный зум, на котором
в народных картах нет конфликта. Так как у организации может быть несколько
`ft_id`, то выбираем минимальный зум среди всех возможных (оптимистичный
сценарий). Считаем, что для зумов меньше минимального у организации показов
нет. Дополнительно конфликты в НЯКе считаются только для определенных зумов
(сейчас с 18 по 21), поэтому для зумов, которые не входят в этот интервал,
считается что показов тоже нет.  
Результаты складываются в таблицу impressions, ее поля:
 - `permalink` - пермалинк организации
 - `impressions_N` - показывается ли организация на N-ом зуме, зумы с 10 до 21.
0 - показа нет, 1 - показ есть
 - `from_nmaps` - есть ли организация в НЯКе
 - `found_in_ymapsdf` - есть ли организация в `ymapsdf`
 - `indoor_level_id` - ссылка на схему индора (может быть `NULL`)

### Renderer
| Key | Value |
| --- | --- |
| Источник данных | [Результаты обстрела POI](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/renderer_impressions/)|
| | [Подготовленные данные о геопродукте на YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/protected_geo_product/impressions/geoproduct_info) |
| Impressions | В папке на [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/protected_geo_product/impressions/renderer) |

С помощью YQL запроса в sandbox таске делается выжимка из таблицы impressions,
но только для геопродуктовых организаций. Обстрел рендерера происходит для всех
POI на карте в рамках (этого проекта)[https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/statistics/impressions].

### Причины непоказов
В итоговой таблице impressions некоторые организации не имеют ни одного показа.
Это может происходить по разнообразным причинам, график причин непоказов можно
увидеть [тут](https://datalens.yandex-team.ru/kalqabqb04ikg-poi-metrics?tab=Epy).
Какие бывают причины:
 - **Невалидные по справочнику** - в [таком](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/lib/extract_info_mappers.py?rev=7520922#L324)
случае организация вообще не попадает в наши пайплайны
 - **Недавно защищенные** - из-за того, что пайплайны работает не мгновенно,
растаскивают организации не сразу и прочих подобных вещей, организации могут
попасть на подложку не сразу после добавления. Считаем, что если организация
стала защищенной недавно (`is_recently_protected_geo_product`), то она может
не показываться на подложке.
 - **Отфильтрован в static_poi** - отфильтрован в `static_poi`
с [валидной причиной](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/static_poi/bundle.py?rev=7521356#L5)
 - **Нет в Народной карте** - если геопродукт находится только в процессе
добавления в НЯК, то он попадает в карту, как и обычные организации из
`extra_poi_bundle`. При этом они могут конфликтовать, быть под индором и
т.п., и поэтому не показываться. [Подробности](https://st.yandex-team.ru/GEOQ-447)
 - **Нет в ymapsdf по неизвестной причине** - выяснение причин [тут](https://st.yandex-team.ru/GEOQ-431)
 - **Выставлен disp_class 10** - в Народной карте можно выставить `ignore`
у организации, тогда у нее будет `disp_class` 10, и она не будет показываться
на подложке. Подробнее [тут](https://st.yandex-team.ru/GEOQ-435).
 - **Перекрыто indoor слоем** - у части организаций все показы перекрываются
индором.
 - **Нет в рендерере по неизвестной причине** - такие организации обычно
конфликтуют с чем-то.

