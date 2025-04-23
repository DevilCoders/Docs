# CDP-CH-WRITER
Писатель данных о клиентах и заказах CDP в ClickHouse.
Описание CDP можно прочитать тут - https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/README.md

## Описание
`cdp-ch-writer` - процессинговый сервис, отвечающий за запись данных о клиентах и заказах CDP в ClickHouse. Данные из ClickHouse
используются в `cdp-api` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-api/README.md)) и
`cdp-intapi` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-intapi/README.md)) для реализации сегментации
клиентов CDP и в `cdp-segments-evaluator` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-segments-evaluator/README.md))
для вычисления идентификаторов посетителей Яндекс.Метрики (UserID) попавших в тот или иной сегмент.


### Deployment
production - https://deploy.yandex-team.ru/stages/cdp-ch-writer-production

testing - https://deploy.yandex-team.ru/stages/cdp-ch-writer-test

### Какие данные потребляет?
`cdp-ch-writer` читает данные ключи клиентов и заказов записанные
`cdp-core` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-core/README.md)),
`cdp-scheduler` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-scheduler/README.md)),
`cdp-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-matcher/README.md)) и
`cdp-cryptaid-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-cryptaid-matcher/README.md))
 из двух консюмеров
в Logbroker:
1. Консюмер, из которого читаются ключи клиентов - `updated-clients-consumer` (`message ClientKey`)
2. Консюмер, из которого читаются ключи заказов - `updated-orders-consumer` (`message OrderKey`)

Данные едут в формате protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-common/proto/cdp.proto)

### Как обрабатывает данные?
#### Ключи клиентов
В `cdp-ch-writer` обработка ключей клиентов состоит из этапов:
1. Прочитать по ключам состояния клиентов из базы. Таблица в YDB `clients_data/clients`. Её пишет
`cdp-core` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-core/README.md))
2. Прочитать по ключам соответствующие данному клиенту UserID. Таблица в YDB `matching/client_user_id`. Её пишет
`cdp-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-matcher/README.md))
3. Прочитать по ключам соответствующие данному клиенту CryptaID. Таблица в YDB `matching/client_crypta_id`. Её пишет
`cdp-cryptaid-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-cryptaid-matcher/README.md))
4. Прочитать по ключам соответствующие данному клиенту GluedYuid. Таблица в YDB `matching/client_glued_yuid`. Её тоже пишет
`cdp-cryptaid-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-cryptaid-matcher/README.md))
5. Посчитать для клиентов агрегаты по их заказам. Данные о заказах пишутся в
`cdp-core` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-core/README.md))
6. **Атомарно** инкрементировать версию клиента в базе. Таблица в YDB `ch_writer_meta/client_versions`.
7. Объединить все прочитанные данные в подготовленный объект клиента, который позже будет записан в базу в ClickHouse.

#### Ключи заказов
1. Прочитать по ключам состояния клиентов из базы. Таблица в YDB `clients_data/orders`. Её пишет
`cdp-core` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-core/README.md))
2. **Атомарно** инкрементировать версию заказа в базе. Таблица в YDB `ch_writer_meta/order_versions`.
3. Объединить все прочитанные данные в подготовленный объект заказа, который позже будет записан в базу в ClickHouse.

### Куда пишет данные?
Данные клиентов и заказов записываются в ClickHouse:
1. Таблица с клиентами - `clients_d`
2. Таблица с заказами - `orders_d`

#### ReplacingMergeTree
Каждая запись клиента или заказа при записи в ClickHouse имеёт свою уникальную (для данного клиента или заказа) версию.
В свою очередь таблицы, в которые пишутся клиенты и заказы, имеют в ClickHouse движок ReplacingMergeTree
([документация ClickHouse](https://clickhouse.tech/docs/en/engines/table-engines/mergetree-family/replacingmergetree/)).
Эти два фактора совокупности дают возможность "обновлять" строчки в ClickHouse. Ограничением такого подхода является то,
что запросы в такие таблицы необходимо делать с FINAL([документация ClickHouse](https://clickhouse.tech/docs/en/sql-reference/statements/select/from/# select-from-final)).

## Графики
Графики для production:
1. [Мониторинг консюмера `updated-clients-consumer` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/updated-clients-consumer)
2. [Мониторинг консюмера `updated-orders-consumer` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/updated-orders-consumer)





