# Сервис отправки данных подписчикам (Dispatcher)

Обрабатывает сообщения из QYT [dispatcher/queue](https://yt.yandex-team.ru/markov/navigation?path=//home/market/production/indexer/datacamp/dispatcher/queue) в формате [UnitedOffersSubscriptionMessage](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/subscription/subscription.proto).

QYT данные дампятся в логброкер топик [dispatcher-qyt-dump](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/dev/dispatcher-qyt-dump)

Читает указанные в сообщении офера из хранилища и рассылает подписчикам.

## Метрики

- [Сводный дашборд](https://nda.ya.ru/t/jFqv9oTi4qCuzy)
- Мониторинги хоста в деплое
  - [прод](https://deploy.yandex-team.ru/stages/production_market_datacamp-dispatcher/monitoring)
  - [престейбл](https://deploy.yandex-team.ru/stages/prestable_market_datacamp-dispatcher/monitoring)
  - [тестинг](https://deploy.yandex-team.ru/stages/testing_market_datacamp-dispatcher/monitoring)
- Количество обработанных оферов
  - [прод](https://yasm.yandex-team.ru/chart/itype=marketdatacampdispatcher;hosts=ASEARCH;ctype=prestable,production;signals=unistat-SubscriptionDispatcher_offers_processed_dmmm/?range=7200000)
  - [тестинг](https://yasm.yandex-team.ru/chart/itype=marketdatacampdispatcher;hosts=ASEARCH;ctype=testing;signals=unistat-SubscriptionDispatcher_offers_processed_dmmm/?range=7200000)
- Статистика отправки подписчикам
  - [прод](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_Subscribers_prod/)
  - [тестинг](https://yasm.yandex-team.ru/template/panel/Market_Datacamp_Subscribers_testing/)
- Дашборд QYT
  - [прод](https://solomon.yandex-team.ru/?project=big_rt_queue_daemon&dashboard=queue_lags_and_rate&cluster=markov&l.consumer=dispatcher&l.queue=%2F%2Fhome%2Fmarket%2Fproduction%2Findexer%2Fdatacamp%2Fdispatcher%2Fqueue&b=7d&e=)
  - [тестинг](https://solomon.yandex-team.ru/?project=big_rt_queue_daemon&dashboard=queue_lags_and_rate&cluster=markov&l.consumer=dispatcher&l.queue=%2F%2Fhome%2Fmarket%2Ftesting%2Findexer%2Fdatacamp%2Fdispatcher%2Fqueue&b=7d&e=)
- Топики с дампом данных QYT для расследований
  - [прод](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/dev/dispatcher-qyt-dump)
  - [тестинг](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/dev/dispatcher-qyt-dump-testing)

## Траблшутинг
- Найти отправку офера можно через qyt-dump [logfeller](https://yql.yandex-team.ru/Operations/YsU-ELq3kz5HKt8ZXDemydWNv07ICoIEQXH_ZXmIYmE=) по business_id, offer_id.

## Выходные топики
- ```market-indexer/*/blue/datacamp-partner-stock```
    - Назначение: Топик с партнерскими стоками для передачи в StockStoarge через MBI по push-модели
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```piper```
    - Потребители: ```MBI```
    - Testing [```market-indexer/testing/blue/datacamp-partner-stock```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/blue/datacamp-partner-stock)
    - Production [```market-indexer/prod/blue/datacamp-partner-stock```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-partner-stock)

- ```market-indexer/*/united/datacamp-offers-to-miner```
    - Назначение: united-офферы (синие и белые), отправленные на майнинг
    - Формат: ```Market::DataCamp::DatacampMessage::united_offers```
    - Поставщики: ```piper, scanner, routines, blue/stroller, white/stroller```
    - Потребители: ```blue/miner, united/miner```
    - Testing [```market-indexer/testing/united/datacamp-offers-to-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-offers-to-miner)
    - Production [```market-indexer/prod/united/datacamp-offers-to-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-to-miner)

- `saas/services/market_datacamp/*/topics/*`
    - Назначение: документы на индексацию в сервис SaaS, для поиска офферов в ПИ
    - Формат: ```NRTYServer::TMessage```
    - Поставщики: ```piper, blue/stroller, white/stroller```
    - Потребители: ```saas```
    - Testing [```saas/services/market_datacamp/prestable_market_idx/topics/*```](https://lb.yandex-team.ru/logbroker/accounts/saas/services/market_datacamp/prestable_market_idx/topics)
    - Production [```saas/services/market_datacamp/stable/topics/*```](https://lb.yandex-team.ru/logbroker/accounts/saas/services/market_datacamp/stable/topics)


- ```market-indexer/*/united/iris-msku-controllers-to-miner```
    - Назначение: msku на обогащение офферным составом (маппингами), содержимым msku. MARKETINDEXER-38020
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```piper, scanner, routines```
    - Потребители: ```united/miner```
    - Testing [```market-indexer/testing/united/iris-msku-controllers-to-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/iris-msku-controllers-to-miner)
    - Production [```market-indexer/prod/united/iris-msku-controllers-to-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/iris-msku-controllers-to-miner)


- ```market-indexer/*/united/datacamp-offers-stocks```

  - Назначение: Результат парсинга стоков из ссылочных фидов
  - Формат: ```Market::DataCamp::DatacampMessage```
  - Поставщики: ```united/qparser```
  - Потребители: ```piper```
  - Testing [```market-indexer/testing/united/datacamp-offers-stocks```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-offers-stocks)
  - Production [```market-indexer/prod/united/datacamp-offers-stocks```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-stocks)
