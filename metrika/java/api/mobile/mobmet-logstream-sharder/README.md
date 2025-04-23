# mobmet-logstream-sharder
Некоторые владельцы приложений с АппМетрикой хотят свои данные. Они активируют себе выгрузку через Logs Stream API,
и события их приложений попадают в топик `appmetrica-export-logstream-events`, который пишется движком. Этот демон
читает топик и делит приложения на малые (nano) и большие (giga) и пишет в соответствующие два топика:
`appmetrica-export-logstream-nano` и `appmetrica-export-logstream-giga`. Топик nano пошардирован по APIKey,
а топик giga - по DeviceIDHash. Потреблять эти топики будет mobmet-logstream-writer.

[формат protobuf](https://a.yandex-team.ru/arc/trunk/arcadia/metrika/core/libs/appmetrica/protos/export/appmetrica_event.proto)
