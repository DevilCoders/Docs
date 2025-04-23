# Подробное руководство для лога операций биллинга

## Мотивация создания
До этого существовал [лог транзакций биллинга](https://wiki.yandex-team.ru/users/ruslansd/Log-tranzakcijj-Billinga), но появилась необходимость осуществить переезд на yt.
При этом возникла идея улучшить модель. Модель была немного реструктурирована и обогащена информацией

## Поставки
На стороне биллинга таска [BillingOperationPushTask](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-tms/logic/src/tasks/BillingOperationPushTask.scala?rev=r9539924#L23) пушит события в брокер.
Далее брокер осуществляет поставку данных в yt и кафку.

### Поставка в yt
- Данные сначала попадают во временную таблицу [billing_raw_operation_event](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/billing/billing_raw_operation_event/1d).
- Во временной таблице данные партиционируются по полю [timestamp](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9532537#L427). [Подробнее о партиционировании](https://docs.yandex-team.ru/classifieds-infra/broker/configuration#repartitioning).
- Во временной таблице содержатся данные за последние 30 дней ([настройка в схеме](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9558371L418)).
- Из временной таблицы данные перепартиционируются в основную таблицу [billing_operation_event](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d). [Подробнее о перепартиционировании](#перепартиционирование-данных-в-yt).
- В основной таблице данные хранятся вечно.
- [Время появления событий в YT – не RT](https://docs.yandex-team.ru/classifieds-infra/broker/design#garantiya-dostavki).
- Гарантия at-least-once delivery.

### Поставка в кафку
- Данные попадают в топик `broker-billing-billing-raw-operation-event`.
- Гарантия at-least-once delivery.

## Перепартиционирование данных в yt
Из временной таблицы ([billing_raw_operation_event](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/billing/billing_raw_operation_event/1d)) данные перепартиционируются по полю [operation_timetamp](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9558371L429) в основную таблицу ([billing_operation_event](https://yt.yandex-team.ru/hahn/navigation?path=//home/verticals/broker/prod/warehouse/billing/billing_operation_event/1d)).

Подробнее про гарантии перепартиционирования можно прочитать в [доке брокера](https://docs.yandex-team.ru/classifieds-infra/broker/configuration#repartitioning).
Посмотреть настройки перпартиционирования можно в [схеме](https://a.yandex-team.ru/arcadia/classifieds/schema-registry/proto/vertis/billing/billing-event.proto?rev=r9532537?rev=r9558371L419).
