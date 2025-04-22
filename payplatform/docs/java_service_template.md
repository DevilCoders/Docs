Шаблон micronaut-микросервиса
=============================

Данная библиотека представляет собой базовый модуль для разработки микросервисов на базе `micronaut`. На данный момент из коробки предоставляется:

- Запуск сервера
- Сконфигурированное окружение
- Ручка `/ping`
- Поддержка tvm
- Логирование входящих/исходящих запросов из коробки

Использование
-------------

Для использования модуля необходимо подключить его в качестве зависимости в ya.make приложения и настроить annotation processors.

```makefile
INCLUDE(${ARCADIA_ROOT}/payplatform/java/common.inc) # подключаем общие зависимости и параметры сборки

PEERDIR(
    payplatform/java/service # подключаем шаблон приложения
)

# настраиваем annotation processors
ANNOTATION_PROCESSOR(
    io.micronaut.annotation.processing.TypeElementVisitorProcessor
    io.micronaut.annotation.processing.AggregatingTypeElementVisitorProcessor
    io.micronaut.annotation.processing.PackageConfigurationInjectProcessor
    io.micronaut.annotation.processing.BeanDefinitionInjectProcessor
    io.micronaut.annotation.processing.ServiceDescriptionProcessor
)
```

Настройка логирования запросов
------------------------------

По-умолчанию логируются все входящие и исходящие запросы. При этом удаляется содержимое заголовков:

- Authorization
- Proxy-Authorization
- X-Ya-Service-Ticket
- X-Ya-User-Ticket

Для более точечной настройки необходимо создать бин одного из типов библиотеки `logbook` (`PEERDIR contrib/java/org/zalando/logbook-core`):

- QueryFilter
- PathFilter
- HeaderFilter
- BodyFilter
- RequestFilter
- ResponseFilter

Docker
------

Для пакетирования в docker необходимо использовать базовый образ [registry.yandex.net/payplatform-micronaut-java-base](https://a.yandex-team.ru/arc/trunk/arcadia/payplatform/java/base_image), который заточен под запуск приложений на базе `micronaut`. Подробности [здесь](base_java_image.md).

Пример
------

Пример приложения можно посмотреть в папке [example](https://a.yandex-team.ru/arc/trunk/arcadia/payplatform/java/service/example).
