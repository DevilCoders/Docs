# mbo-common

Библиотека общих классов для различных сервисов mbo

Что можно добавлять в библиотеку:
- Константы, не связанные с хранилищем моделей (например, [Language.java](src/main/java/ru/yandex/market/mbo/common/model/Language.java) )
- Классы доступа к внешним сервисам (например, [ShopsProvider.java](src/main/java/ru/yandex/market/mbo/common/mbi/ShopsProvider.java) )
- Утилитарные классы, не относящиеся напрямую к mbo (например, [ImageUtils.java](src/main/java/ru/yandex/market/mbo/common/image/ImageUtils.java) )

Что нельзя добавлять в библиотеку
- Класс CommonModel. Допустимо работать только с protobuf моделями и параметрами
- Классы, специфичные для выбранного хранилища (yt, yql)
- Визуальные классы для gwt (для этого есть common-gwt)

# Релиз

Публикация производится через таск https://teamcity.yandex-team.ru/viewType.html?buildTypeId=Market_Mbo_MboCommonRelease
