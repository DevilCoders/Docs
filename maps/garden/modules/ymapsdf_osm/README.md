# ymapsdf_osm

## Общее описание модуля

Модуль предназначен для конвертации картографических данных из
[формата OSM](https://wiki.openstreetmap.org/wiki/PBF_Format) в
[формат YMapsDF 2.0](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/about.html).

Данный модуль аналогичен модулю [ymapsdf](https://a.yandex-team.ru/arc/trunk/arcadia/maps/garden/modules/ymapsdf),
конвертирующему данные НЯК.


## Архитектура

Часть функций модуля реализована в отдельных компонентах:
* [road_graph_osm_to_ymapsdf](https://a.yandex-team.ru/arc_vcs/maps/garden/libs/osm/road_graph_osm_to_ymapsdf) - первичная
обработка данных (формирование таблицы `object_details`) и построение дорожного графа
(формирование таблиц `rd*`, `vehicle_restriction*`, `cond*`)
* [libymapsdf](https://a.yandex-team.ru/arc_vcs/maps/garden/libs/ymapsdf) - общая с модулем `ymapsdf` реализация


## Входные данные

Входные данные подготавливаются следующими модулями:
* [osm_src](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/osm_src) - регистратор ресурса PBF файла планеты
* [osm_borders_src](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/osm_borders_src) - границы стран и регионов,
формирование coverage файлов
* [osm_coastlines_src](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/osm_coastlines_src) - гидрография
* [osm_to_yt](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/osm_coastlines_src) - нарезка планеты на регионы,
конвертация PBF в YT таблицы
* [altay](https://a.yandex-team.ru/arc_vcs/maps/garden/modules/osm_src) - таблица rubrics

Данные OSM поступают на вход модуля в виде YT - таблиц:
* `nodes` (точки)
* `nodes_tags` (теги к точкам)
* `ways` (линии)
* `ways_nodes` (составные для линии точки)
* `ways_tags` (теги к линиям)
* `relations` (объединения элементов)
* `relations_tags` (теги к объединениям)
* `relations_members` (элементы, входящие в объединения)

Данные OSM для планеты обновляются автоматически
[sandbox задачей](https://a.yandex-team.ru/arc_vcs/maps/garden/sandbox/osm_downloader).
Далее, обновленные данные поступают на вход модуля osm_src в результате периодического сканирования ресурсов.


## Этапы сборки

### Первичная обработка данных
Данные для всех объектов OSM объединяются во временной таблице `object_details`. Для объектов всех типов
извлекаются теги (колонка `tags`) и ссылки на дочерние объекты (колонка `members`). Построение таблицы производится в
несколько этапов:
* Для объектов типа `NODE` и `WAY` вычисляется геометрия в формате WKB-HEX (колонка `shape`). Объекты `NODE` имеют тип
геометрии `Point`, объекты `WAY` - `LineString`. 
* Данные дополняются геометрией объектов типа `RELATION`. Геометрия `RELATION` вычисляется
путем полигонизации геометрии дочерних объектов типа `WAY` с ролями `inner` и `outer`. Объекты `RELATION` имеют тип
`Polygon` или `MultiPolygon`. Если объект `RELATION` не имеет дочерних путей, значение shape объекта остается `NULL`.
Если для объекта `RELATION` не удается вычислить геометрию полигона из дочерних путей, такие объекты отбрасываюся с
записью информации в лог ошибок (здесь и далее: таблица log_bad_osm + stderr задачи). Если для объекта `RELATION`
геометрия вычислена только частично (полигон построен только из части дочерних путей), такой объект сохраняется с
записью информациии в лог ошибок.
* Данные дополняются геометрией гидрографии. Объекты гидрографии сохраняются с кастомным типом `COASTLINE` и кастомными
тегами, для последующей конвертации в соответствующие ft объекты.


### Построение дорог
Документация:
* https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/road_graf_introduction.html
* https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/ymapsdf/garden/create/rd.sql
* https://wiki.openstreetmap.org/wiki/RU:Key:highway

Логика:
1. Пути с тегом `highway` разрезаются на отдельные участки в местах пересечений, 
т.к. дорожный граф в `ymapsdf` является планарным, пересечения дорог на одном z-уровне не допускаются.
2. Отдельные участки дорог группируются по именам и геометрической близости и объединяются дороги
в (`rd`, `rd_geom`, `rd_rd_el`).
3. На основе тегов участков дорог вычисляются имена дорог (`rd_nm`).
4. На основе геометрии дороги вычисляется её центр (`rd_center`) и привязка к единице АТД (`rd_ad`).
5. Исокод участка дороги вычисляется по геометрическому вхождению в страну.
6. Исокод дороги вычисляется на основе исокодов участков этой дороги.


### Создание таблиц ad
Документация:
* https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/ad.html
* https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/ymapsdf/garden/create/ad.sql
* https://wiki.openstreetmap.org/wiki/RU:Tag:boundary%3Dadministrative
* https://wiki.openstreetmap.org/wiki/Map_features#Populated_settlements.2C_urban

На основе построенного в модуле `osm_borders_src` кавереджа по странам рассчитываются исокоды для всех
объектов из `object_details` и создается `object_details_with_isocodes`.

Из данных `object_details_with_isocodes` заполняются таблицы `ad`, `ad_center`, `ad_geom`, `ad_nm`, `locality`.
На этом этапе геометрия стран заменяется на геометрию, полученную в модуле `osm_borders_src`.
Для попадания в `ad*` таблицы объект OSM должен обладать следующими свойствами:
* тип объекта `NODE`, `WAY` или `RELATION`
* тип геометрии `Point`, замкнутый `LineString`, `Polygon` или `Multipolygon`
* объект должен иметь имя (см. [Имена объектов](#Имена объектов))
* установлен один из тегов `boundary=administrative`, `place`, `capital`

В промежуточной таблице `ad`:
* level_kind:
    - 1 - `boundary=administrative` и `admin_level=2`
    - 2 - `boundary=administrative` и `admin_level=4`
    - 3 - `place` имеет значение `region`, `province`, `district`, `county`, `municipality`
    - 4 - `place` имеет значение `city`, `town`, `village`, `hamlet`, или `capital` имеет занчение `yes`, `4`
    - 5 - `place` имеет значение `borough`, `suburb`
    - 7 - `place` имеет значение `quarter`, `neighbourhood`, `city_block`


Для некоторых стран настроен алгоритм определения `level_kind` по тегу `admin_level` и исокоду OSM объекта. Значение
`admin_level` интерпретируется в соответствии с
["admin_level=* Country specific values"](https://wiki.openstreetmap.org/wiki/Tag:boundary%3Dadministrative#admin_level.3D.2A_Country_specific_values)

При невозможности определения `level_kind` объект не попадает в таблицу `ad`.

* isocode:
    - значение тега `ISO3166-1:alpha2` для `level_kind=1` (страна)
    - для остальных объектов исокод рассчитывается по попаданию в кавередж по странам

* search_class:
    - `NULL` - по умолчанию
    - 10 - исключить из coverage (объекты с самопересечением, см. [Проблемы](#Проблемы))

* Остальные поля - по умолчанию

Для точечных объектов объектов городов (`level_kind`=4) не имеющих границы, граница генерируется из геометрии
близлежащих дорог и безымянных дорожных элементов. Дороги находящиеся внутри существующих городских границ
исключаются из алгоритма генерации с использованием coverage. После генерации дополнительных городских границ,
производится повторное построение coverage с использованием этих границ.

Таблица `ad_geom` заполняется данными shape OSM объекта. Для стран геометрия заменяется геометрией от модуля
osm_borders_src.

Таблица `ad_center` вычисляется из данных shape OSM объекта.

На основе промежуточной таблицы ad создается full coverage (см. [Построение coverage](#Построение coverage)).

В таблице ad заполняются поля `p_ad_id` по вложенности геометрий АД друг в друга.

Заполняется таблица `ad_nm` (см. [Имена объектов](#Имена объектов)).

После формирования `ad*` таблиц производятся следующие проверки (см. [Автотесты](#Автотесты)):
* каждый объект в `ad` дожен иметь минимум одно имя в `ad_nm`
* для каждого объекта `ad` должна быть определена геометрия в `ad_geom`
* каждый ключ `p_ad_id` в `ad` должен указывать на существующий объект
* проверка наличия всех стран для региона по исокодам
* проверка наличия столиц для всех стран
* TODO: производится выборочная проверка наличия значимых объектов: областей, столиц, крупных городов
* производится сравнение количества объектов `ad` сгруппированых по `level_kind` (TODO: +группировка по `isocode`) с
предыдущим билдом. Если предыдущий билд не существует, проверка считается успешной. При обнаружении существенных
расхождений с предыдущим билдом генерируется исключение `DataValidationWarning`:
    - любые изменения количества объектов c `level_kind` 1 (страна)
    - изменение количества объектов более чем на 0.5% для объектов с `level_kind` 2 (штат/область)
    - изменение количества объектов более чем на 2% для остальных значений `level_kind`


### Создание таблиц ft
Документация:
* https://wiki.openstreetmap.org/wiki/Map_features

Логика:

Объекты `ft` формируются из объектов `object_details` на основе анализа и конвертации тегов OSM в поле `ft_type_id`
таблицы `ft` (см. [типы картографических объектов](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/ft_type.html)).
Если не удается установить `ft_type_id` однозначно (тегам соответствует несколько значений), для объекта выбирается
наименьшее значение, информация об объекте записывается в лог ошибок. Теги участвующие в формировании `ft` объектов:
* [aeroway](https://wiki.openstreetmap.org/wiki/Map_features#Aeroway) - аэропорты
* [leisure](https://wiki.openstreetmap.org/wiki/Map_features#Leisure) - досуг и спорт
* [amenity](https://wiki.openstreetmap.org/wiki/Map_features#Amenity) - городские объекты, организации
* [office](https://wiki.openstreetmap.org/wiki/Map_features#Office) - офисы
* [shop](https://wiki.openstreetmap.org/wiki/Map_features#Shop) - магазины
* [tourism](https://wiki.openstreetmap.org/wiki/Map_features#Tourism) - отели, туризм
* [religion](https://wiki.openstreetmap.org/wiki/Key:religion) - религиозные объекты
* [natural](https://wiki.openstreetmap.org/wiki/Map_features#Natural) - природные объекты
* [railway](https://wiki.openstreetmap.org/wiki/Map_features#Railway) - железные дороги
* [waterway](https://wiki.openstreetmap.org/wiki/Map_features#Waterway) - водоёмы


### Создание таблиц bld
Документация:
* https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/bld.html
* https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/ymapsdf/garden/create/bld.sql
* https://wiki.openstreetmap.org/wiki/Buildings

Логика:
1. Из OSM-объектов с типом `WAY` и тэгом `building` формируются таблицы `bld` и `bld_geom`.
2. На основании вхождения точки с адресом в геометрию здания создается таблица `bld_addr`.


### Создание таблиц addr
Документация:
* https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/adr.html
* https://a.yandex-team.ru/arc/trunk/arcadia/maps/doc/schemas/ymapsdf/garden/create/addr.sql
* https://wiki.openstreetmap.org/wiki/Addresses

Логика:
1. Из OSM-объектов с тэгами `addr:housenumber` и `addr:street` создаются таблицы `addr` и `addr_nm`.
2. Полученные адресные точки добавляются в таблицу `node`.

Детали реализации:
Для создания таблицы addr также требуются готовые таблицы `rd`, `ad`, `ft`.


### Построение coverage
TODO


### Объединение геометрии
TODO


## Детали реализации

### Нумерация объектов
При формировании объектов ymapsdf сохраняется связь между исходным объектом OSM и объектом ymapsdf. Связь реализована
через механизм генерации идентификаторов (id) ymapsdf из идентификатора и типа OSM объекта. Из-за того, что в OSM
уникальность id обеспечивается только в пределах типа, в ymapsdf для каждого типа OSM выделен отдельный диапазон id.
Размер всех диапазонов одинаковый, т.о. тип исходного объекта можно определить операцией деления ymapsdf id на размер
диапазона. Для обеспечения возможности приязки нескольких объектов ymapsdf к одному объекту OSM, внутри каждого
диапазона выделены поддиапазоны id.

Пример:
```py
# при range_size = 1_000_000_000_000, way_range_start = 2_000_000_000_000, way_subrange_size = 10_000_000_000
ymapsdf_id = 2_030_000_000_456
osm_type = ymapsdf_id / range_size                      # 2 - WAY
osm_id = (ymapsdf_id % range_size) % way_subrange_size  # 456
osm_link = "https://www.openstreetmap.org/way/456"
index = (ymapsdf_id % range_size) / way_subrange_size   # 3 - четвертый объект ymapsdf на данном объекте OSM
```


### Имена объектов
Документация:
* https://wiki.openstreetmap.org/wiki/Key:name
* https://wiki.openstreetmap.org/wiki/Multilingual_names

Логика:

Таблицы имен объектов ymapsdf `ad_nm`, `addr_nm`, `rd_nm`, `ft_nm` формируются из OSM тегов `name`, `official_name`,
`alt_name`.

Значение поля `name_type` устанавливается исходя из имени тега:
* 0 (официальное) - для тега `official_name`
* 1 (для подписывания) - для тега `name`
* 4 (синоним) - для тега `alt_name`

Установка поля `lang`:
* Если язык имени задан в теге, значение берется из тега
* Если язык имени не задан в теге, значение вычисляется библиотекой maps/libs/locale как официальный язык страны по
`isocode` объекта 
* Если не удалось вычислить значение по `isocode`, устанавливается значение по умолчанию: "en"

Установка поля `is_local`:
* true - если значение языка не указано в теге, или если значение языка указанное в теге совпадает с вычисленным по
`isocode`
* false - во всех остальных случаях


### Автотесты

После формирования финальных таблиц ymapsdf, данные таблиц валидируются специальными задачами - автотестами. Автотесты
не производят финальных таблиц. Результатом работы автотестов может быть успешное завершение или генерация исключений
типа [AutotestFailedError](https://docs.yandex-team.ru/garden/module-exceptions#autotestsfailederror) или
[DataValidationWarning](https://docs.yandex-team.ru/garden/module-exceptions#datavalidationwarning).
Исключение типа DataValidationWarning генерируется при обнаружении некритичных проблем в данных (например при
подозрительных изменениях в статистике), и может быть проигнорировано в UI огорода.


## Статистика конвертации данных

На основе полученных таблиц `ad`, `addr`, `bld`, `rd`, `ft`, `rd_el`, `cond` собирается статистика по количеству
сгенерированных объектов разных типов. Также из таблицы `log_bad_osm` собирается статистика по количеству
объектов, парсинг которых прошел неудачно. Вся эта информация попадает в таблицу `statistics`, после чего
она добавляется в конец в таблицу [`all_statistics`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/ymapsdf_osm/all_statistics).
Для каждого контура создается своя таблица `all_statistics`. Отдельная задача в sandbox-e по крону запускает сортировку
`all_statistics` -> `all_statistics_sorted` в стабильном контуре для оптимизации последующего её сканирования.

По данным из `all_statistics_sorted` строится дашборд для
[стабильного контура](https://datalens.yandex-team.ru/60qyl2afztxex-statistika-konvertacii-dannyh-openstreetmap-v-ymapsdf).


## Проблемы

При конвертации данных OSM возникает множество проблем. Общий подход к решению проблем на данный момент - некорректные
объекты во входных данных игнорируются (отбрасываются) с записью информации в лог ошибок и в YT таблицы для последующего
анализа. Некритичные проблемы во входных данных не должны блокировать сборку всего модуля, т.к. источник данных нам не
подконтролен и исправление данных нами невозможно или крайне затруднено.

Многие из проблем связаны с такими особенностями Open Street Map как:
* слабая модерация и валидация (ошибки во входных данных)
* слабая спецификация (много способов сделать одно и то же)
* региональные особенности (разные правила картографирования в различных регионах, см. например
[admin_level](https://wiki.openstreetmap.org/wiki/Tag:boundary%3Dadministrative#admin_level.3D.2A_Country_specific_values))

Проблемы:
* Отсутствие языка в локальных именах
(см. [multinngual names](https://wiki.openstreetmap.org/wiki/Multilingual_names)). В качестве временного workaround язык
для локальных имен сейчас вычисляется по ISOCODE.

* Существующий механизм построения coverage ([coverage5](https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/coverage))
не работает с объектами (административными границами) имеющими самопересечение (внешняя граница полигона касается сама
себя, или соприкасаются внутренние полигоны). Для НЯК эта проблема решается исправлением данных на карте. В ymapsdf_osm
такие объекты в данный момент не участвуют в вычислении coverage.
Из крупных административных границ не попадающих в coverage - это
[Германия](https://www.openstreetmap.org/relation/51477#map=14/47.5642/10.4671) (Бавария). Так же в coverage не
попадают множество городов в северной Америке. Возможные варианты решения проблемы:
    - доработка libcoverage
    - исправление самопересечений в геометрии адм. границ модулем ymapsdf_osm для coverage

* Некорректные данные OSM, например:
    - [дубликат дочернего объекта (Версия #4)](https://www.openstreetmap.org/relation/935770/history)
    - [линия из одной точки (Версия #7)](https://www.openstreetmap.org/way/36814269/history)
    - [адрес дома "Горького улица", название улицы "улица Горького" (Версия #2)](https://www.openstreetmap.org/way/268578149/history)
    - [в адресе дома улица имеет имя "1" (Версия #2)](https://www.openstreetmap.org/way/178603504/history)
    - [дом с указанием улицы и деревня одновременно (Версия #7)](https://www.openstreetmap.org/way/682222935/history)

* Неоднозначные данные OSM, например:
    - [город и озеро в одном объекте (Версия #5)](https://www.openstreetmap.org/way/102297078/history)
    - [дорога и парк в одном объекте (Версия #11)](https://www.openstreetmap.org/way/4360419/history)
    - [здание задано точкой (Версия #2)](https://www.openstreetmap.org/node/8655167895/history)
    - [пример сложной геометрии здания (Версия #2)](https://www.openstreetmap.org/relation/11822213/history)
    - [дорога, у которой прописан номер дома (Версия #2)](https://www.openstreetmap.org/way/249815687/history)
    - [здание и туннель в одном объекте (Версия #16)](https://www.openstreetmap.org/way/450732440/history)
    - [здание и дорога в одном объекте (Версия #9)](https://www.openstreetmap.org/way/33302331/history)
    - дубликаты АТД: [1](https://www.openstreetmap.org/relation/2036205), [2](https://www.openstreetmap.org/way/482007050)

{% note info %}

Проанализировать проблемные объекты можно с помощью таблицы `log_bad_osm`.
У каждой записи имеется флаг `error_level` со следующими возможными значениями:
* info - ошибка не является критической и не повлияла значительно на созданный ymapsdf-объект
* warn - ошибка привила к частичному изменению (отбрасыванию) свойств ymapsdf-объекта по сравнению с исходным OSM-объектом
* crit - ошибка привела к невозможности создания ymapsdf-объекта на основании исходного OSM-объекта

{% endnote %}
