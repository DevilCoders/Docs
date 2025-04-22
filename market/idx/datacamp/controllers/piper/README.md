# Асинхронный контроллер оферного хранилища(Piper)

Микросервис оферного хранилища, отвечающий за обработку оферов, поступающих из логброкера

Читаем данных из различных топиков и транзакционно складывает данные в хранилище в DYT

## YT

### Тайминги апдейтера
Testing - https://yasm.yandex-team.ru/panel/krasnobaev._zrrlkv

Production - https://yasm.yandex-team.ru/panel/krasnobaev._rb1IC_


### Белый

Testing - https://yt.yandex-team.ru/pythia/navigation?path=//home/market/testing/indexer/datacamp/white&

Production - https://yt.yandex-team.ru/markov/navigation?path=//home/market/production/indexer/datacamp/white&

## Nanny

Ассинхронный контроллер живет полностью в RTC

### Белый

Дашборд в няне - https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/market_indexer_datacamp_piper/

Потребление ресурсов в головане - https://yasm.yandex-team.ru/template/panel/market-porto/itype=marketdatacamppiper;ctype=production;prj=market/

## Deploy

### ЦУМ

https://tsum.yandex-team.ru/pipe/projects/indexer/delivery-dashboard/datacamp-controllers

### Руками

1. ```ya package pkg.json```
2. ```ya upload --type=MARKET_DATACAMP_PIPER_APP {tar_gz_name}```
3. go to link from prev step, click "Task ID", click "Release"->"Testing"|"Prestable"|"Production"
4. go to link from sandbox info log(```SANDBOX_RELEASE_<ID>_<ENV>```), choose services and click "Activate"


## Topics

[Лаги](https://solomon.yandex-team.ru/?project=kikimr&cluster=lbk&service=pqtabletAggregatedCounters&l.host=*&l.TopicPath=*&l.OriginDC=*&l.ConsumerPath=market-indexer%2Fprod%2Fwhite%2Fdatacamp-consumer-original&l.sensor=MessageLagByCommitted&graph=auto&b=1h&e=) чтения из топиков

- [Схема](https://wiki.yandex-team.ru/users/evlyubimov/presentations/united-blue/) использования топиков для интеграции синего в Единое Офферное Хранилище

- [```mbi/prod/market-quick```](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/market-quick?group=all&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original)

  - Топик с API данными от партнеров всех цветов
  - Формат: ```Market::DataCamp::SyncAPI::ChangeOfferRequest```
  - Поставщиком данных является ```MBI```
  - Потребители: ```blue/piper, white/piper, united/piper, saashub```

- [```mbi/prod/supplier-promo-offer```](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/supplier-promo-offer)
  - Назначение: Топик с промоакциями от MBI (для массовой настройки параметром участия в акции)
  - Формат: ```Market::DataCamp::DatacampMessage```
  - Поставщики: ```MBI```
  - Потребители: ```blue/piper, united/piper```

- [```market-mbo/prod/deepmind/offer-hidings-topic```](https://lb.yandex-team.ru/logbroker/accounts/market-mbo/prod/deepmind/offer-hidings-topic)
  - Назначение: Топик со скрытиям MBO-разум
  - Формат: ```Market::DataCamp::DatacampMessage```
  - Поставщики: ```MBO```
  - Потребители: ```blue/piper, united/piper```

- [```market-indexer/prod/blue/stock-storage```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/stock-storage?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1579682380511&metricsTo=1579768780511)

  - Назначение: Топик с информацией о стоках
  - Формат: ```Market::DataCamp::SyncAPI::ChangeOfferRequest```
  - Поставщики: ```Stock-Storage```
  - Потребители: ```blue/piper, united/piper```

- [```market-indexer/prod/blue/datacamp-offers```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-offers?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original)

  - Содержит сериализованные офера в формате [DatacampOffer](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto)
  - Поставщики: ```blue/miner, blue/stroller```
  - Потребители: ```blue/piper```

- [```market-indexer/prod/blue/datacamp-qoffers```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-qoffers)

  - Назначение: Результат парсинга офферов синим qparser
  - Формат: ```Market::DataCamp::DatacampMessage```
  - Поставщики: ```blue/qparser```
  - Потребители: ```blue/piper, united/piper```

  - [```market-indexer/prod/united/datacamp-qoffers-upload-update```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/market-indexer/prod/united/datacamp-qoffers-upload-update)

  - Назначение: Отдельный топик для upload/update фидов MARKETINDEXER-40270
  - Формат: ```Market::DataCamp::DatacampMessage```
  - Поставщики: ```qparser```
  - Потребители: ```piper```

- [```market-indexer/prod/blue/datacamp-messages```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-messages?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original)

  - Содержит сериализованные офера в формате [DatacampMessage](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/DatacampMessage.proto)
  - Поставщиком данных является [blue/push-parser](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/parser) и [blue/qparser](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/feeds/qparser)
  - Потребители: ```blue/piper, united/piper```

- [```market-indexer/prod/blue/datacamp-offers-to-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-offers-to-miner?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original)

  - Назначение: Топик с офферами, отправленными на майнинг
  - Формат: ```Market::DataCamp::OffersBatch```
  - Поставщики: ```blue/piper, blue/stroller, blue/scanner, blue/routines```
  - Потребители: ```blue/miner```

- [```market-indexer/prod/blue/datacamp-offers-batch-to-saashub```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-offers-batch-to-saashub?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original)

  - Назначение: Quick data для RTY через saashub
  - Формат: ```Market::DataCamp::OffersBatch```
  - Поставщики: ```blue/piper, blue/stroller, blue/scanner```
  - Потребители: ```saashub```

- [```market-indexer/prod/blue/datacamp-partner-stock```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-partner-stock)
  - Назначение: Топик с партнерскими стоками для передачи в StockStoarge через MBI по push-модели
  - Формат: ```Market::DataCamp::DatacampMessage```
  - Поставщики: ```blue/piper, united/piper```
  - Потребители: ```MBI```

- [```market-indexer/prod/white/datacamp-offers-blog```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/white/datacamp-offers-blog?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original)

  - Назначение: Содержит вспомогательную информацию об офере(ошибки обработки, ...)
  - Формат: ```OfferBlog```
  - Поставщики: ```white/push-parser, white/piper, white/miner, white/scanner, white/stroller```
  - Потребители: ```white/piper```

- [```market-indexer/prod/white/datacamp-messages```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/white/datacamp-messages?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original)

  - Назначение:
    - Технические команды ```Market::DataCamp::DatacampMessage::tech_command``` от ```white/push-parser```
    - united-офферы ```Market::DataCamp::DatacampMessage::united_offers``` после майнинга через ```united/miner```
  - Формат: ```Market::DataCamp::DatacampMessage```
  - Поставщики: ```united/miner, white/push-parser```
  - Потребители: ```united/piper```

- [```market-indexer/prod/white/offers-to-saashub```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/white/offers-to-saashub?group=own&page=statistics&type=topic&tab=readMetrics&shownTopics=all%20topics&topicCluster=all%20original&consumer=market-indexer%2Fprod%2Fblue%2Fdatacamp-consumer-original)

  - Назначение: XXX
  - Формат: YYY
  - Поставщики: ZZZ
  - Потребители: WWW

- [```market-indexer/prod/united/datacamp-offers-to-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-to-miner)

  - Назначение: united-офферы (синие и белые), отправленные на майнинг
  - Формат: ```Market::DataCamp::DatacampMessage::united_offers```
  - Поставщики: ```united/piper, blue/stroller, blue/scanner, blue/routines, white/stroller, white/scanner, white/routines```
  - Потребители: ```blue/miner, united/miner```

- [```market-indexer/prod/united/datacamp-offers-from-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-from-miner)

  - Назначение: united-офферы, после майнинга
  - Формат: ```Market::DataCamp::DatacampMessage::united_offers```
  - Поставщики: ```blue/miner```
  - Потребители: ```united/piper```

- [```mbi/prod/internal-market-quick```](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/internal-market-quick)
  - Назначение: Топик со скрытиями/ценами от MBI (скрытия не партнерские, а маркетные => internal market)
    - На момент создания apr-2021 передаются данные о скрытиях для синих офферов из-за превышения цены.
  - Формат: ```Market::DataCamp::DatacampMessage```
  - Поставщики: ```MBI```
  - Потребители: ```united/piper```


## Useful links

- [Графики](https://solomon.yandex-team.ru/?cluster=seneca-sas&project=yt&dashboard=yt-artemis-bundle&service=yt_node_tablet_profiling&b=1h&e=&l.tablet_cell_bundle=market-datacamp-production) нагрузки бандлов YT

- [Графики](https://solomon.yandex-team.ru/?project=yt&cluster=markov&dashboard=yt-ui-user-request-load-new&service=yt_master&user=robot-mrkt-idx-prod&b=365d&e=) нагрузки мастер YT

- [Самодиагностика](https://wiki.yandex-team.ru/yt/userdoc/selfdiag/) DYT
