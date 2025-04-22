# FrameworksConverter

FrameworksConverter – вспомогательная библиотека для сборки xcframework-ов и генерации spm-пакета c ними. Изначально была написана для сборки cocoapods зависимостей и подключения их через spm в проект auto.ru.

Поскольку потребности у разных проектов могут отличаться и отдельные зависимости могут требовать специальной обработки, FrameworksConverter не предоставляет универсального механизма по сборке фреймворков, вместо этого предоставляются переиспользуемые "шаги сборки", из которых можно сформировать процесс сборки под свои нужды. "Шаги сборки" представляют объекты, которые получает массив urls, производят какую-либо обработку над файлами/папками и возвращают новый массив urls. Конечно, можно писать и свои шаги.

## Как использовать

Создать spm пакет c executableTarget, добавить зависимость от FrameworksConverter, написать реализацию [`BuildStrategy`](https://a.yandex-team.ru/arcadia/classifieds/mobile-autoru-client-ios/FrameworksConverter/Sources/FrameworksConverter/BuildStrategy.swift) [пример реализации](https://a.yandex-team.ru/arcadia/classifieds/mobile-autoru-client-ios/ThirdPartyConverter/Sources/ThirdPartyConverter/ThirdPartyBuildStrategy.swift), добавить атрибут @main на реализацию.

Пример использования можно посмотреть [здесь](https://a.yandex-team.ru/arcadia/classifieds/mobile-autoru-client-ios/ThirdPartyConverter)