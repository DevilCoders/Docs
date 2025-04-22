# coverage_geoid

В Яндексе иерархия объектов административно-территориального деления (АТД) поддерживается независимо в 2х местах: в [Геобазе][geobase] и в [Народной карте][nmaps]. В каждой из систем используются свои идентификаторы (далее `geobaseId` и `adId`). В каждой - хранится геометрия регионов и различные метаданные.

Данные из Народной карты доступны в формате `ymapsdf` в [таблицах ad_* в YT][adtables].

Наиболее точная геометрия - в Народной карте. Картографы следят за её актуальностью.

Разработчики Геобазы время от времени обновляют у себя геометрию данными из НЯК. Цепочка доставки данных: НЯК -> ymapsdf -> экспорт геокодера -> Геобаза.

Привязка geobaseId <-> adId хранится на стороне НЯК и экспортируется в таблицу `ad_source` в `ymapsdf`. Картографы следят за актуальностью привязки.

## Слой geoid

Частая задача - найти geobaseId по географическим координатам (долгота, широта). Для этого в библиотеке `libgeobase` поддерживается метод [lookup::region_id_by_location][lookup]. Однако, в Геобазе геометрия может быть устаревшей и не точной.

В Картах поддерживается свой механизм решения этой задачи.

Огородный модуль `coverage_geoid` ежедневно варит файл `geoid.mms.1` в формате библиотеки [coverage][coverage], который содержит слой `geoid`. Найти geobaseIds по географическим координатам можно с помощью метода [Layer::regionIds][regionIds].

Этот слой также доступен через сервис `meta`. Пример запроса: http://core-meta.maps.yandex.net/layers?action=info&l=geoid&ll=55.763375,37.620308

Есть библиотека [geoinfo][geoinfo], которая является обёрткой над [coverage][coverage] и Геобазой и предоставляет более удобный API. Эта библиотека также доступна в YQL-запросах через [UDF][udf].

## Геометрия

Геометрия регионов берётся из свежего `ymapsdf` и в общем случае может отличаться от геометрии из Геобазы.

В модуле `coverage_geoid` захардкожен расчёт геометрии для регионов, связанных с городами федерального подчинения.

Пример: регион geobaseId=1 "Москва и Московская область" в Геобазе содержит геометрию только Московской области без Москвы. В слое `geoid` геометрия этого региона включает также Москву.

## Деплой данных

Файл `geoid.mms.1` распространяется 3мя путями:

* через датасет [yandex-maps-coverage5-geoid][yandex-maps-coverage5-geoid] в экстатике.
* через файл в YT - поддерживается симлинк [//home/maps/core/garden/prod/coverage_geoid/latest/geoid.mms.1][latest].
* через ресурс [MAPS_CORE_COVERAGE_GEOID][sandbox] в Sandbox.

## Обнаружение ошибок в данных (autotests_failed)

При возникновении ошибки в данных, следует написать в телеграм чат [maps-content-monitorings][maps-content-monitorings] 
и поставить длительный даунтайм, с расчетом на то, что в течение этого времени выкатят исправления в данных.

[geobase]: https://doc.yandex-team.ru/lib/libgeobase5/concepts/about.html
[nmaps]: https://n.maps.yandex.ru/
[adtables]: https://yt.yandex-team.ru/hahn/navigation?filter=ad&path=//home/maps/core/garden/prod/ymapsdf/latest/cis1
[lookup]: https://doc.yandex-team.ru/lib/libgeobase5/concepts/interfaces-cplusplus-lookup.html#interfaces-cplusplus-lookup__meth-region_id_by_location
[coverage]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/coverage
[regionIds]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/libs/coverage/include/yandex/maps/coverage5/layer.h#L82
[geoinfo]: https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/libs/geoinfo
[udf]: https://a.yandex-team.ru/arc/trunk/arcadia/yql/udfs/maps/geoinfo
[yandex-maps-coverage5-geoid]: http://ecstatic.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions
[latest]: https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/coverage_geoid/latest/geoid.mms.1
[sandbox]: https://sandbox.yandex-team.ru/resources?type=MAPS_CORE_COVERAGE_GEOID&limit=20&attrs=%7B%22garden_contour%22%3A%22stable%22%7D&created=14_days
[maps-content-monitorings]: https://t.me/joinchat/HL-Tmf4WxyRmZDc6
