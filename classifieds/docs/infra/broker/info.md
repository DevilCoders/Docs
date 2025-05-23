# Брокер

## Общие сведения

Брокер – это сервис для гарантированной доставки типизированных данных до долговременных хранилищ (YT, ClickHouse) и до персистентных очередей сообщений (Kafka, Logbroker) с единой точкой конфигурирования.

Если у вас есть любые вопросы - заходите в наш [Чат поддержки](https://t.me/joinchat/Rf9HXgmSuEGxW6YB).

## Гарантии

Брокер предоставляет `at-least-once` гарантии доставки, если клиент при записи дожидается ack от брокера. В противном случае данные могут быть утеряны.

Порядок сообщений не гарантируется.

## Сценарии использования

1. **Долговременное хранение данных** (например, логов или счетчиков) для аналитики.

2. **Межсервисное взаимодействие**. Использовать брокер только как замену Kafka большого смысла нет (у второго гораздо больше возможностей), но можно бесплатно получить вывод в Kafka, если данные уже пишутся в брокер для других целей. Также брокер можно рассматривать в качестве альтернативы клиенту записи в Logbroker, если не требуются exactly-once гарантии доставки.

## Начало работы

Для начала работы поставщику требуется сделать несколько действий:

1. Описать формат сообщения в [schema-registry](https://a.yandex-team.ru/arc_vcs/classifieds/schema-registry). Вмержить изменения в схеме, дождаться обновления версии роботом.
Брокер работает только с форматом [protobuf](https://developers.google.com/protocol-buffers). Подробности в разделе про [схему](schema_guide.md) данных.

2. Указать [настройки](configuration.md) для брокера.

3. Начать слать данные в API.

{% note warning %}

Если поставка ожидается крупной (более 1к rps или больше 2 мб/с), необходимо заранее предупредить нас об этом через тикет в [VSDATA](https://st.yandex-team.ru/createTicket?queue=VSDATA).

{% endnote %}


## API

Для отправки в брокер используется [grpc api](https://a.yandex-team.ru/arc_vcs/classifieds/schema-registry/blob/master/proto/broker/api/broker.proto).
У сервиса есть Consul DNS `broker-api-grpc-api.query.consul` и envoy-балансеры `broker-api-grpc-api.vrts-slb.{test|prod}.vertis.yandex.net`. Предпочтительным является Consul DNS.

* Тайминги. Брокер рассчитан на пропускную способность, а не на тайминги отправки одного сообщения. Поэтому если вам нужно ждать ack от сервера, то убедитесь, что вы согласны ждать до нескольких секунд.
На текущие тайминги можно посмотреть на [графике](https://grafana.vertis.yandex-team.ru/d/ybtbWWaZz/broker-api?orgId=1&refresh=1m&from=now-1h&to=now&fullscreen&panelId=56&var-datasource=Prometheus&var-job=broker-api&var-instance=All&var-window=2m)

* Размер сообщения. Брокер не принимает сообщения больше 4 мб.

* Возраст сообщения. По умолчанию сообщения старше 7 дней не принимаются.

## Сравнение с другими решениями

### Запись в Logbroker напрямую

Logbroker предоставляет только сложный API с установкой сессии и ручной работой с sourceId/seqNo. В Java SDK нет поддержки [Cluster Discovery Service](https://logbroker.yandex-team.ru/docs/concepts/data/cds), поэтому управление приоритетами между датацентрами тоже на клиенте. Для простых случаев fire-and-forget API брокера выглядит проще.
Также в Logbroker отсутствует валидация присылаемых данных.

### Поставка в YT через Logfeller

Logfeller ничего не знает про формат данных, поэтому клиент должен явно складывать файл с File Descriptor Set рядом с настройками парсера и следить за его актуальностью.

### Поставка в другие хранилища через Data transfer

Поставка в ClickHouse доступна только через копирование полного снепшота, репликации нет. Нельзя посталять в ClickHouse только часть полей.
Поставки в Kafka из LogBroker нет.
