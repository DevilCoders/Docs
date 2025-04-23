# Сетевая и прикладная инфраструктура Яндекса (в контексте наших приложений)

## TODO - Секретница Yav

TODO Сделать клиент

## TODO - Yandex Deploy

## TODO - BlackBox

## TODO - Tanker

## TODO - [Puncher](https://puncher.yandex-team.ru/)

## TODO - [RackTables](https://racktables.yandex-team.ru/index.php?page=services&tab=projects&project_name=_TRAVEL_BIZDEV_ADMIN_TEST_NETS_)

## TODO - XXXXX

https://st.yandex-team.ru/HRTECH-38
https://a.yandex-team.ru/arcadia/hrtech/frontend/a.yaml

## [Sandbox](https://sandbox.yandex-team.ru)

Единый инструмент для запуска задач и хранения артефактов

-   [Таск для сборки Node 18](https://sandbox.yandex-team.ru/task/1311747953/view)
-   [Таск для сборки Node 12](https://sandbox.yandex-team.ru/task/1270268832/view)

## [Awacs](https://nanny.yandex-team.ru/ui/#/awacs/)

Отвечает за:

-   Домены
-   Сертификаты
-   Балансировку
-   Проксирование запросов к инстансам, развернутым в Yandex Deploy

Неймспейсы фронтенда:

-   [Production (внутренний)](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-prod-internal-balancer/show)
-   [Testing](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-testing-balancer/show)

## [TVM](https://wiki.yandex-team.ru/passport/tvm2)

-   [Общее - https://wiki.yandex-team.ru/passport/tvm2](https://wiki.yandex-team.ru/passport/tvm2)
-   [TVM-демон - https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon)
-   [Про ServiceTicket`ы - https://wiki.yandex-team.ru/passport/tvm2/stbrief/](https://wiki.yandex-team.ru/passport/tvm2/stbrief/)

Используется для двусторонней верификации запросов между сервисами.
Допустим, наш сервис `App` хочет слать запросы в апи (`Api`)

-   `App` должен иметь свой TVM ID
-   `Api` должен иметь свой TVM ID
-   `App` должен указать, что он знает о сервисе `Api` у себя в tvm-конфигурации (указать его ID)
-   `Api` должен указать, что он знает о сервисе `App` у себя в tvm-конфигурации (указать его ID)
-   При запросе `App` должен запросить у своего TVM-демона Service Ticket для сервиса `Api` и добавить его в заголовок
-   При входящем запросе `Api` должен прочесть токен и спросить у своего TVM-демона, валиден ли этот токен

### Инструменты

-   Локальные
    -   [yandex-net/core/tvm](../libs/yandex-net/core/tvm) - Предоставляет платформо-независимый TVM-клиент
    -   [codegen](../libs/codegen/readme.md#a-namelocal-tvma-tvm) - Генератор для запуска локального TVM-демона
        ```shell
        yarn g dev local-tvm
        ```
-   TODO yandex-passport-tvmtool
