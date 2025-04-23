## Деплой sandbox-ресурсом

Для деплоя используется [универсальный docker-контейнер](https://a.yandex-team.ru/arc/trunk/arcadia/mail/docker-images/mailfront-base)
с обвязкой (nginx, logs, etc), sandbox-ресурс с приложением и sandbox-ресурс с конфигами (nginx, monrun, etc).

Конфиги собираются локально `make upload-settings` в случае, когда меняется конфиг обвязки (`docker/fs`),
после сборки нужно поменять id соответствующего ресурса в `.config/ps-deploy*`.

Sandbox-ресурс варится при сборке тестовых стендов и релизов.
Для тестовых стендов тип ресурса [MAILFRONT_COMPONENT_QA](https://sandbox.yandex-team.ru/resources?type=MAILFRONT_COMPONENT_QA&limit=20&attrs=%7B%22component%22%3A%22maya%22%7D), время жизни 30 дней.
Production-сборки типа [MAILFRONT_MAYA](https://sandbox.yandex-team.ru/resources?type=MAILFRONT_MAYA&limit=20), время жизни бесконечно.
