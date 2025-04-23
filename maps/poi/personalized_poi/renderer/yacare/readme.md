## Основные характеристики
* При старте сервиса загружает в память все персональные POI из ecstatic датасета
* По OAuth токену при помощи blackbox узнает puid пользователя
* Рендерит тайлы через DataSource
* Поддерживает эксперименты через дополнительные параметры с префиксом experimental

## Ручки рендерера

### Внешние
* /version возвращает версию используемого датасета
* /tiles (tile, version, locale, l, pbversion, scale, [zmin,zmax:optional]) возвращает тайл последней версии
    * tile – координаты запрашиваемого тайла
    * version – запрашиваемая версия (игнорируется, всегда возвращается самая свежая)
    * locale – локаль для подписей
    * l – название слоя (должно быть personalized_poi)
    * scale – запрашиваемый зум
    * zmin,zmax - параметры мультизума
* /icons (scale, id) возвращает иконку
    * scale - запрашиваемый зум
    * id – идентификатор иконки (хеш-код от содержимого иконки)
* /glyphs (font_id, range) возвращает шрифт
    * font_id - имя шрифта
    * range - идентификатор первого и последнего глифов

### Внутренние
* /reload_poi (poi_dataset_version) загружает в память свежий датасет
    * poi_dataset_version - значение, которое будет возвращаться ручкой /version
* /reload_design загружает в память свежий дизайн из датасета
* /admin (...) - позволяет сменить уровень логирования, см. подробнее [реализацию](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/renderer/yacare/lib/yacare_server.cpp)
* /switch_to_* - отладочные ручки

## Мультизум
* Ручка `/tiles` поддерживает мультизум. 
* На фиксированном сценарии, в котором последовательно запрашивались зумы с 13-го по 18-й, мультизумный эксперимент с ренжами `[13-14], [15-19]` показал меньше запросов:
```
without multizoom:

mlevkov@flss44zwf6upvte7.man.yp-c.yandex.net: 91
mlevkov@q5panjmbcx3hmfcb.vla.yp-c.yandex.net: 87
mlevkov@zs6um2rhx5zzar5f.sas.yp-c.yandex.net: 87


with multizoom:

mlevkov@zs6um2rhx5zzar5f.sas.yp-c.yandex.net: 18
mlevkov@q5panjmbcx3hmfcb.vla.yp-c.yandex.net: 21
mlevkov@flss44zwf6upvte7.man.yp-c.yandex.net: 21
```
* [Стрельбы](https://lunapark.yandex-team.ru/GEOQ-200) со сравнением старого и нового вариантов (существенной деградации не выявили)
* Детали реализации на клиенте можно посмотреть в [тикете](https://st.yandex-team.ru/GEOQ-200)