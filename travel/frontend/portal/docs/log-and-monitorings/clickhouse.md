# Clickhouse

У Путешествий есть свой [кластер ClickHouse](https://yc.yandex-team.ru/folders/foo33m9g9m98lqipih8r/managed-clickhouse/cluster/mdbkale9qiarbrho8f69/view) во внутрениим облаке.

Этот кластер ClickHouse используется для:

-   хранения технических метрик о непосредственной работе приложения (runtime логи и данные, например статистика по API запросам)
-   метрик около работы приложения (релизные измерения)

## Пользователи

-   Для каждой базы мы заводим [нового пользователя](https://yav.yandex-team.ru/secret/sec-01e6bdgg9dr1jsb57y8f6jcdh8/explore/versions) с доступом только к этой базе.
-   Логины и пароли текущих пользователей лежат в [секретнице](https://yav.yandex-team.ru/secret/sec-01e6bdgg9dr1jsb57y8f6jcdh8/explore/versions).
-   Все новые пользователи так же должны быть добавлены в секретницу
