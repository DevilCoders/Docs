# coverage_geoid_deployment

Модуль активирует в экстатике датасет [yandex-maps-coverage5-geoid](http://ecstatic.maps.yandex.net/pkg/yandex-maps-coverage5-geoid/versions).

Посмотреть толерантность активации датасета в экстатике можно в конфигах:
* [stable](https://a.yandex-team.ru/arc_vcs/maps/config/ecstatic/stable/yandex-maps-coverage5.conf)
* [datatesting](https://a.yandex-team.ru/arc_vcs/maps/config/ecstatic/datatesting/coverage5.conf)

Модуль выставляет симлинк [latest](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/coverage_geoid/latest/geoid.mms.1) в YT.

Модуль релизит ресурс [MAPS_CORE_COVERAGE_GEOID](https://sandbox.yandex-team.ru/resources?type=MAPS_CORE_COVERAGE_GEOID&limit=20&attrs=%7B%22garden_contour%22%3A%22stable%22%7D&created=14_days) в Sandbox.
