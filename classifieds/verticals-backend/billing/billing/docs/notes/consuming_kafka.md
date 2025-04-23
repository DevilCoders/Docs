# Чтение сырых событий биллингом из кафки

Биллинг читает несколько топиков кафки с сырыми событиями, которые впоследствии обилливаются.

## Топики billing-event-log и broker-billing-event-to-pay

Основные топики сырых событий. Авто в эти топики шлет все услуги (размещения, поднятия), недвижка еще помимо услуг шлет показы телефонов (phone_show).

Топик _billing-event-log_ -- легаси, все клиенты в последствии должны слать события через брокер, чтобы оно попадало в топик _broker-billing-event-to-pay_.
Отправка событий через брокер лучше, потому что так события попадают в YT.

Оба этих топика содержат прото-мессаджи [EventMessage](https://a.yandex-team.ru/arc_vcs/classifieds/schema-registry/proto/vertis/hydra/event_model.proto?rev=r9253252#L19), которые на самом деле являются нетипизированными _map<string, string>_.

Консьюмеры топиков билдится [здесь](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-events-storage/src/main/scala/ru/yandex/vertis/billing/events/backend/MysqlEngine.scala#L228-L229?rev=r9253252).
В них события парсятся с помощью [EventParser](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-events-storage/src/main/scala/ru/yandex/vertis/billing/events/model/EventParser.scala#L27?rev=r9253252),
и [записываются в MySQL](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-dao/src/main/scala/ru/yandex/vertis/billing/service/impl/EventStoreServiceImpl.scala?rev=r9253252).
Для сырых событий есть отдельная база данных [_vs_bill_storage_](https://idm.yandex-team.ru/#rf-role=cK4gcdZ9#h2p/mysql/mdbjec6l5cui21o8a3kh/vs_bill_storage/ro,rf-expanded=cK4gcdZ9,rf=1), в которой каждый тип события записываются в [разные таблицы](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-dao/src/main/resources/sql/vs_billing_events_storage.final.sql?rev=r9253252).


## Топик telepony-call-changes

Топик телепоневских звонков с прото-мессаджами [TeleponyCall](https://a.yandex-team.ru/arc_vcs/classifieds/schema-registry/proto/vertis/telepony/call_model.proto?rev=r9253252#L14).

Потреблением звонков занимается [TeleponyCallKafkaConsumer](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-tms/logic/src/backend/TeleponyCallKafkaConsumer.scala?rev=r9253252).
Внутри него звонки [преобразуются во внутреннее представление CallFact](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-tms/logic/src/event/call/telepony/TeleponyCallProcessor.scala#L28?rev=r9253252)
и записываются в MySQL в [таблицу callfact](https://a.yandex-team.ru/arcadia/classifieds/verticals-backend/billing/billing/billing-tms/logic/src/event/call/telepony/TeleponyCallProcessor.scala#L57?rev=r9253252).
