[GEOQ-646](https://st.yandex-team.ru/GEOQ-646) — Сколько популярных организаций непоказывается?
===

Хотим посмотреть как много популярных организаций (то бишь с высоким `dispClass`ом) не отображаются. Например, [Агонь]((https://yandex.ru/maps/org/agon/126455508136/?ll=60.598868%2C56.836268&z=18)) с `dispClass` 4.8 на карте отсутствует. Интересно как много таких случаев, что может быть причиной, и критично ли это.

Для этого анализируем [exta_poi_bundle]((https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/extra_poi_bundle/stable_v2/)) и [renderer_impressions]((https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/renderer_impressions)). В первой табличке хранится информация о поях, в том числе dicpClass, во второй информация о том, на каких зумах организация отрисовывается. Пои с `is_indoor_covered` не учитываются, так как "renderer impressions не детектирует корректно показы в зданиях с indoor слоем" @tswr.

## Немного об имплементации
`main.py` делает 3 вещи:
1. Inner Join `exta_poi_bundle` и `renderer_impressions` по id организации и заодно фильтрует организации с `is_indoor_covered` и преобразует колонки.
2. Запускает `script.yql, который создает две таблицы:
    * [check_poi_stats]((https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/users/iambackend/check_poi_rendering/check_poi_stats)) – статистика по разным `dispClass`ам о том, сколько поев среди них не отображаются. dispClass округлен до первого знака.
    * [unshown](https://yt.yandex-team.ru/hahn/navigation?offsetValue=999&path=//home/maps/users/iambackend/check_poi_rendering/unshown) – отсортированный по `dispClass`у список неотображаемых организаций.
3. Создает `easyview.yson` с топ-1000 организаций, которые не отображаются для дальнейшего запуска [easyview](https://a.yandex-team.ru/arc/trunk/arcadia/maps/tools/easyview). 
