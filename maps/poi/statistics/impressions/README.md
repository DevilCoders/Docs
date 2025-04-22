Показы POI 
===

## Общая информация

Проект предназначен для выяснения факта показа POI на различных зумах. Для
выяснения факта показа используется два основных источника: BEBR логи и тайлы
рендерера. Показы по BEBR логам берутся уже из готовой таблицы
[org_statistics](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/data/org_statistics)
(она варится в пайплайне [Personalized poi](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder/extractor/extract_from_analytics.py)), тайлы рендерера берутся путем обстрела рендерера
по всем координатам, где должны находиться POI.

### Информация для потребителей
| Key | Value |
| --- | --- |
| Мейнтейнеры | [Maps.GeoQuality](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) |
| Шедулеры в Sandbox | [Обстрел всех POI](https://sandbox.yandex-team.ru/scheduler/45378/view) <br> [Аналитика показов](https://sandbox.yandex-team.ru/scheduler/78697/view) |
| ABC сервис | [POI impressions checker](https://abc.yandex-team.ru/services/maps-core-poi-impressions-checker/) <br> [Статистика POI](https://abc.yandex-team.ru/services/maps-core-poi-statistics/) |
| Таблицы на YT | [Результаты обстрела](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/renderer_impressions/) |
| Связанные проекты | [Аналитика популярных зон](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/statistics/yellow_zones) <br> [Показы геопродукта](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/statistics/protected_geo_product/impressions) <br> [Представительские метрики](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/statistics/representative_metrics) |
| Графики | [Аналитика показов POI](https://datalens.yandex-team.ru/kalqabqb04ikg-poi-metrics?tab=409) <br> [Представительский график](https://datalens.yandex-team.ru/kalqabqb04ikg-poi-metrics?tab=MWa) <br> [Показы геопродукта](https://datalens.yandex-team.ru/kalqabqb04ikg-poi-metrics?tab=Epy) <br> [Показы популярных зон](https://datalens.yandex-team.ru/kalqabqb04ikg-poi-metrics?tab=bKR) |

## Технические детали

### Renderer
| Key | Value |
| --- | --- |
| Источник данных | Тайлы рендерера на http://core-renderer-tiles.maps.yandex.net |
| | [Таблица orginfo](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/data/orginfo) |
| Результаты обстрела рендерера | В папке на [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/renderer_impressions/)

Бинарь `process_tiles` производит обстрел рендерера. Для того, чтоб не
пришлось забирать тайлики со всего мира, мы берем только координаты из таблицы
orginfo - поля ymapsdf_lat и ymapsdf_lon. Для каждой такой координаты мы
определяем нужный тайл, после чего формируется список уникальных тайлов нужный
для получения информации о всех POI. Каждый такой тайл запрашиваем у
рендерера на ручке `vmap2/tiles`, а если знаем, что это indoor организация, то
дополнительно запрашиваем тайл с ручки `indoor/tiles`. На текущий момент
multizoom не используется, и в каждом тайле у нас информация только на каком-то
одном зуме. Чтоб начать использовать multizoom потребуется доработка либы
[mapcheck2](https://a.yandex-team.ru/arc/trunk/arcadia/maps/renderer/tools/mapcheck2/lib),
которую мы используем для получения и парсинга тайлов.

В sandbox таске поход в рендерер происходит с помощью TVM тикетов. Приложение
обстрела рендерера [тут](https://abc.yandex-team.ru/services/maps-core-poi-impressions-checker/resources/?show-resource=26322453),
ходим в stable кэша рендерера [сюда](https://abc.yandex-team.ru/services/maps-core-renderer-cache/resources/?show-resource=23610858).
Рейтлимит в рендерере для нас выставлен в [2500 RPS](https://a.yandex-team.ru/arc/trunk/arcadia/maps/config/ratelimiter/maps_core_renderer_cache/stable.yaml),
но так как при срабатывании рейтлимитера он сразу на несколько секунд начинает
присылать 429, то себя мы сами ограничиваем до 2400 RPS - посмотреть это можно в
[панельке](https://yasm.yandex-team.ru/template/panel/maps_core_renderer_cache-ratelimiter2-panel?range=7200000).  
[Подробнее](https://wiki.yandex-team.ru/passport/tvm2/quickstart/#1-sozdajomprilozhenie)
о TVM, тикетах и как это все работает.

Из всех полученных тайлов мы получаем список организаций, которые были на этих
тайлах, и складываем его во временную таблицу на YT.
Поля таблицы:
 - `permalink` - пермалинк организации
 - `zoom` - зум тайла, с которого была получена эта организация
 - `is_indoor_covered` - был ли организации тэг `indoor_covered`.
Тэг означает, что сверху есть индор, который эту организацию перекрывает.
Исключение составляют организации на 16 зуме - у них тэг `indoor_covered`
есть, но индор на таком слое не показывается.

Для каждого тайла создаются уникальные записи для всех организаций, что
были на этом тайле. То есть организация может встречатся в таблице
несколько раз: на разных зумах и в индор/не-индор тайлах.

После этого с помощью бинаря `merge_zooms` из таблиц `orginfo` и
результата обстрела формируется итоговая таблица impressions на
[YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/statistics/renderer_impressions/).
Поля таблицы:
 - `date` - дата обстрела
 - `permalink` - пермалинк организации
 - `impressions_N` - показывается ли организация на N-ом зуме, зумы с 10 до 21.
0 - показа нет, 1 - показ есть
 - `is_indoor_covered` - был ли у этой организации показ (на любом зуме),
который перекрывается индором

Просто берутся все уникальные организации из `orginfo` и для каждой
проставляются impressions на соответствующем зуме, если хотя бы один не
перекрытый индором показ на этом зуме был. Для `is_indoor_covered` наоборот,
если хотя бы один показ на любом зуме был перекрыт индором, то выставляется
в `True`. Все это с учётом того, что на 16 зуме организация может быть
показана без настоящего перекрытия индором, но с `indoor_covered` тэгом.
