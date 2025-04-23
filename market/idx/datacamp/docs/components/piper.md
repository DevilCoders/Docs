
## Piper

Микросервис, обрабатывающий сообщения из logbroker. Читает данные из различных топиков и транзакционно складывает их в YT. Написан на основе C++ фреймворка common proxy.

## Графики
* Основной дашборд
  - [production](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_PiperWhite_stable/?range=86400000)
  - [тестинг](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_PiperWhite_testing/?range=86400000)
* Дашборд потребления ресурсов
  - [production](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdatacamppiper;ctype=production;prj=market/)
  - [prestable](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdatacamppiper;ctype=prestable;prj=market/)
  - [testing](https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdatacamppiper;ctype=testing;prj=market/)

### Графики чтения отдельных топиков
1. Открываем [Solomon](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&l.host=*&l.TopicPath=*&l.OriginDC=*&l.ConsumerPath=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&l.sensor=ReadTimeLagMs&graph=auto&b=1h&e=)
2. В TopicPath указываем топик, графики которого хотим посмотреть
3. В ConsumerPath для production указываем `market-indexer/prod/white/datacamp-consumer-original`, для тестинга — `market-indexer/testing/white/datacamp-consumer-original`
4. В Sensor указываем нужную метрику, например `ReadTimeLag`, `MessageLagByCommitted`, `CreateTimeLagMsByCommitted`, [подробнее про метрики logbroker](https://logbroker.yandex-team.ru/docs/reference/metrics)

Примеры:
* [ReadTimeLag всех production топиков](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&l.host=*&l.TopicPath=*&l.OriginDC=*&l.ConsumerPath=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&l.sensor=ReadTimeLagMs&graph=auto&b=1h&e=)
* [ReadTimeLag всех testing топиков](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&l.host=*&l.TopicPath=*&l.OriginDC=*&l.ConsumerPath=market-indexer%2Ftesting%2Fwhite%2Fdatacamp-consumer-original&l.sensor=ReadTimeLagMs&graph=auto&b=1h&e=)

## Полезные ссылки
* [Код в аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/piper)
* [Релизный пайплайн](https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/datacamp-controllers)

## Настройки
- [LogLevel](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/piper/etc/united.cfg?rev=8585433&blame=true#L5) - уровень логирования


## Квотирование
Для квотирования данных по топикам используем [rpslimiter](https://rpslimiter.z.yandex-team.ru/records/market/datacamp/configs) и [quoter](https://wiki.yandex-team.ru/users/interrupted/market-quoter/)

### Графики: 
* [Testing Получено Данных](https://yasm.yandex-team.ru/panel/s7and.Market_Datacamp_Piper_Testing_Quoter/)
* [Production Получено Данных](https://yasm.yandex-team.ru/panel/s7and.Market_Datacamp_Piper_Production_Quoter/)
* [Testing Time In Wait](https://yasm.yandex-team.ru/panel/s7and.Market_Datacamp_Piper_Testing_Quoter_TimeInWait/)
* [Production Time In Wait](https://yasm.yandex-team.ru/panel/s7and.Market_Datacamp_Piper_Production_Quoter_TimeInWait/)

### Как с этим работать:
* Как узнать имя квоты для топика: у процессора lb_reader есть параметр [QuotaName](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/piper/etc/united.cfg?rev=6180da3b32d5d5d4bac5a902bff38588e2538691#L68)
* Где поменять значение квоты: https://rpslimiter.z.yandex-team.ru/records/market/datacamp/configs в правом окне найти имя квоты и написать ему новый rps, ctrl+s(!!!) и нажать сохранить

### Как начать ограничивать rps для нового ресурса: 
* https://rpslimiter.z.yandex-team.ru/records/market/datacamp/configs по аналогии слева добавить в нужную секцию новый ресурс, справа добавить его лимиты; 
* У процессора lb_reader входного топика добавить параметр QuotaName, в котором имя квоты из rpslimiter'а, [например](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/piper/etc/amore_processors.cfg?rev=84194c6eb7a1db57f00cda53346da2b0e0164464#L1). На самом деле, главное, чтобы в TDataSet::TPtr, который приходет в процессор quoter'а лежало поле 'quota'.
* В пайпере, чтобы данные квотировались нужно пропускать их через процессор квотера, добавить quoter_processor.cfg(From='Откуда пойдут данные', Type='api_message_batch|datacamp_message|external_message|lb_batch').
* Чтобы прокинуть линки — сделать #include quoter_links.cfg(From='Откуда идут данные', To='Куда', Type='api_message_batch|datacamp_message|external_message|lb_batch'), для lb_reader'а ссылку нужно создать lb_reader_with_quoter_links.cfg(From='имя lb_reader', To='куда')

 Подробнее про типы: 
- api_message_batch — TMessageBatch<Offer>
- datacamp_message — TDatacampMessageObject
- external_message — TMessageBatch<ExternalOffer>
- lb_batch — TLBBatch

Пример:
* [добавление процессора квотера](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/piper/etc/blue_tech_commands_processors.cfg?rev=3183cdb5625af3baf5e640b9987800321e9adb13#L2)
* [добавление ссылок](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/piper/etc/blue_tech_commands_links.cfg?rev=3183cdb5625af3baf5e640b9987800321e9adb13#L2)
* [добавление процессора для lb_batch](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/piper/etc/amore_processors.cfg?rev=3183cdb5625af3baf5e640b9987800321e9adb13#L3)
* [добавление ссылок для lb_batch](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/controllers/piper/etc/amore_links.cfg?rev=3183cdb5625af3baf5e640b9987800321e9adb13#L1)


