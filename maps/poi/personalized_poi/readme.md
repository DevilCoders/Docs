## Проект Personalized POI

Цель: отображать залогиненному пользователю POI организаций, с которыми он
как-либо взаимодействовал, на более обзорных зумах, нежели чем этот POI
отображается на подложке. Примеры взаимодействий: искал, кликал на карточке, был
рядом с включенными яндексовыми приложениями.

## Ключевые компоненты

* [Пайплайн подготовки данных](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/builder)
* [Серверный рендерер](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/personalized_poi/renderer)
* [Слой в MapKit](https://git.yandex-team.ru/gitweb/maps/mapsmobi.git?a=tree;f=libs/mapkit/personalized_poi)

## Клиенты

Поддерживаемые
* [TestApp iOS](https://git.yandex-team.ru/gitweb/maps/mapsmobi.git?a=tree;f=apps/test_app/ios/TestApp/Ppoi)
* [МЯК iOS](https://bb.yandex-team.ru/projects/MAPS/repos/mono/browse/maps/Sources/Services/PersonalizedPoiLayerController.swift)

Deprecated (используют [ручку](https://wiki.yandex-team.ru/maps/mobile/logic/map/personal-poi/) геопоиска вместо рендерера)
* [МЯК android](https://bitbucket.browser.yandex-team.ru/projects/MA/repos/mobile-maps-client-android/browse/maps/yandexmaps/src/main/java/ru/yandex/yandexmaps/personal/poi)
