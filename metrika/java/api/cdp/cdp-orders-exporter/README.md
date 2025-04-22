# CDP-ORDERS-EXPORTER
Писатель данных о заказах CDP, обогащённые в ходе обработки, в Logbroker.
Описание CDP можно прочитать тут - https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/README.md

## Описание
`cdp-orders-exporter` - процессинговый сервис, отвечающий за запись данных о заказах CDP, обогащённые в ходе обработки,
в Logbroker. Эти данные используются в `lambda-visits` для привязки событий о заказах в визиты Яндекс.Метрики.

### Deployment
production - https://deploy.yandex-team.ru/stages/cdp-orders-exporter-production

testing - https://deploy.yandex-team.ru/stages/cdp-orders-exporter-test

### Какие данные потребляет?
`cdp-orders-exporter` читает данные ключи клиентов и заказов записанные
`cdp-core` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-core/README.md)),
`cdp-scheduler` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-scheduler/README.md)),
`cdp-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-matcher/README.md)) и
`cdp-cryptaid-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-cryptaid-matcher/README.md))
 из двух консюмеров
в Logbroker:
1. Консюмер, из которого читаются ключи клиентов - `updated-clients-consumer` (`message ClientKey`)
2. Консюмер, из которого читаются ключи заказов - `updated-orders-consumer` (`message OrderKey`)

Данные едут в формате protobuf - [схема тут](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-common/proto/cdp.proto)

#### Фильтрация входных данных
В отличие от остальных сервисов в CDP, этот процессинговый сервис обрабатывает не все сообщения прочитанные из консюмеров,
данные из которых он потребляет. В силу особенностей необходимых данных, которые будут описаны ниже, при чтении ключей
клиентов (из `updated-clients-consumer`) обрабатываются только данные записанные из
`cdp-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-matcher/README.md)) и
`cdp-cryptaid-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-cryptaid-matcher/README.md)).
Для определения источника данных используется `source_id`, про который можно прочитать в
[документации Logbroker](https://logbroker.yandex-team.ru/docs/concepts/data/write# init)

### Как обрабатывает данные?
Как очевидно хотя бы из названия сервиса, `cdp-orders-exporter` экспортирует именно информацию о заказах. В этот момент
у внимательного читателя может появится вопрос, а зачем сервис потребляет данные из `updated-clients-consumer`, в
которые пишутся ключи обновлённых клиентов? Ответ простой: при экспорте необходимо вместе с информацией о заказах,
записать часть информации о клиентах, а именно наборы сматченных для данного клиента идентификаторов: `user_id`, `crypta_id` и
`glued_uid`. Про матчинг `user_id` можно прочитать в описании `cdp-matcher`
([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-matcher/README.md)), а про матчинг `crypta_id` и
`glued_uids` в описании `cdp-cryptaid-matcher` ([описание](https://a.yandex-team.ru/arc_vcs/metrika/java/api/cdp/cdp-cryptaid-matcher/README.md)).

И так, при чтении любого ключа (клиента или заказа) уже понятно к какому клиенту будут относиться данные, но при чтении
ключа клиента не понятно какие заказы данного клиента нужно экспортировать. На данный момент экспорт устроен таким образом,
что при изменении данных о клиенте, экспортируются заказы созданные за последние 90 дней. Таким образом задачи экспорта данных
при обновлении клиента и экспорта данных при обновлении заказа в целом сводятся к одному и тому же алгоритму экспорта данных,
просто с разным подходом к выбору набора заказов, данные о которых нужно экспортировать.

Подготовка данных для экспорта для конкретного заказа выглядит следующим образом:
1. Прочитать из таблицы `clients_data/orders` в YDB информацию о заказе.
2. Прочитать из таблицы `schema/order_statuses` для счётчика, на котором хранится заказ, маппинг из статуса заказа в тип статуса.
Если для статуса в заказе не определён маппинг, то он не экспортируется. Иначе продолжаем.
3. Прочитать из таблицы `system_data/counters` информацию об идентификаторах целей `cdp_order_in_progress` и `cdp_order_paid` на счётчике.
4. Прочитать из таблицы `orders_export_meta/order_versions` текущее состояние экспорта и обновить его атомарно (про обновление
этого состояния можно прочитать ниже).
5. Прочитать из таблицы `matching/client_user_id` привязанные `user_id` к данному клиенту.
6. Прочитать из таблицы `matching/client_crypta_id` привязанные `crypta_id` к данному клиенту.
7. Прочитать из таблицы `matching/client_glued_uids` привязанные `glued_uid` к данному клиенту.
8. Объединить данные в общий объект, который позже будет записан в Logbroker.

#### Обновление состояния экспорта
В ходе подготовки данных для экспорта происходит обновление состояния экспорта. Для каждого заказа его состояние состоит
из 3х ключевых полей:
1. `version` - инкрементально увеличивающаяся версия экспорта.
2. `in_progress_first_time` - по смыслу это время создания заказа. Оно будет использованно в качетсве времени достижения
цели `cdp_order_in_progress`. Всегда берётся равным `create_date_time` из таблицы `clients_data/orders`. Будучи однажды
запомненным в базу больше никогда не меняется.
3. `paid_first_time` - по смыслу это время оплаты заказа. Оно будет использованно в качестве времени достижения
цели `cdp_order_paid`. Если указан `finish_date_time`, то берётся он. Иначе `update_date_time`. Будучи однажды
запомненным в базу больше никогда не меняется.

Хранение времён (`in_progress_first_time` и `cdp_order_in_progress`) в качестве части состояния экспорта позволяет
добиться неизменности времён достижений целей при повторном экспорте.


### Куда пишет данные?
Данные после экспорта пишутся в топик `orders-export-topic` в Logbroker.
Этот топик через Logfeller [доставляется на YT](https://yt.yandex-team.ru/hahn/navigation?path=//logs/cdp-orders-export-log)


## Графики
Графики для production:
1. [Мониторинг консюмера `updated-clients-consumer` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/updated-clients-consumer)
2. [Мониторинг консюмера `updated-orders-consumer` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/updated-orders-consumer)
2. [Мониторинг топика `orders-export-topic` в Logbroker](https://logbroker.yandex-team.ru/lbkx/accounts/metrika/prod/cdp/orders-export-topic)





