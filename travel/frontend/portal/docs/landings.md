# Лендинги

Самый быстрый и простой способ размещения лендинга - использование связки awacs + s3

###s3

В s3 для размещения лендингов выделенна папка `/landings` в бакете `travel-frontend` (структура бакета в тестинге и проде идентичная).
Каждая папка в `/landings` интерпретируется как отдельный лендинг.

Для работы с s3 можно воспользоваться одним из [клиентов](https://wiki.yandex-team.ru/mds/s3-api/s3-clients/).
Реквизиты для входа:

-   [тестинг](https://yav.yandex-team.ru/secret/sec-01fcyysmags16413ppz6v9888p/explore/versions)
-   [прод](https://yav.yandex-team.ru/secret/sec-01dz0vaar2bcc2b27rdvnt02mp/explore/versions)

###awacs

Для проксирования в s3 настроен [апстрим](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-testing-balancer/upstreams/list/portal-proxy-to-s3-landing/show).
Он содержит в себе логику по проксированию и проставлению базовых заголовков для обеспечения безопасности.
Есть ещё вспомогательный [апстрим](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-testing-balancer/upstreams/list/trailing-slash-landing-redirect/show), который осуществляет редиректы вида `/pro/[name]` -> `/pro/[name]/`. Это необходимо для корректной обработки относительных ссылок на ресурсы.

###Требования к лендингам

-   Папка с лендингом должна содержать файл `index.html`, именно на него будет происходить проксирование при обращении к странице лендинга
-   Папка с лендингом должна содержать все ассеты необходимые для корректной работы лендинга. Обращение к сторонним ресурсам должно быть оправдано, т.к. оно требует внесения правок в CSP политики и может нести риски

###Как добавить лендинг

-   Тестинг
    -   Загрузить лендинг в тестовое окружение s3 `travel-frontend/landings/[name]`
    -   Обновить секции `matcher` добавив `/special/[name]/` в тестовых апстримах `portal-proxy-to-s3-landing` и `trailing-slash-landing-redirect`
    -   Проверить работу лендинга по адресу `https://travel-test.yandex.ru/special/[name]`
-   Прод
    -   Загрузить лендинг в продовое окружение s3 в ту же директорию
    -   Внести аналогичные изменения в продовые апстримы `portal-proxy-to-s3-landing` и `trailing-slash-landing-redirect`
    -   Наслаждаться лендингом по адресу `https://travel.yandex.ru/special/[name]`
