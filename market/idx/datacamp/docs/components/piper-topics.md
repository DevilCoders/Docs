## Входные топики
- ```mbi/*/market-quick```
    - Топик с API данными от партнеров всех цветов
    - Формат: ```Market::DataCamp::SyncAPI::ChangeOfferRequest```
    - Поставщиком данных является ```MBI```
    - Потребители: ```piper, saashub```
    - Testing [```mbi/test/market-quick```](https://lb.yandex-team.ru/logbroker/accounts/mbi/test/market-quick)
    - Production [```mbi/prod/market-quick```](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/market-quick)

- ```mbi/*/supplier-promo-offer```
    - Назначение: Топик с промоакциями от MBI (для массовой настройки параметром участия в акции)
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```MBI```
    - Потребители: ```piper```
    - Testing [```mbi/test/supplier-promo-offer```](https://lb.yandex-team.ru/logbroker/accounts/mbi/test/supplier-promo-offer)
    - Production [```mbi/prod/supplier-promo-offer```](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/supplier-promo-offer)

- ```market-mbo/*/deepmind/offer-hidings-topic```
    - Назначение: Топик со скрытиям от РАЗУМа
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```DEEPMIND```
    - Потребители: ```piper```
    - Testing [```market-mbo/test/deepmind/offer-hidings-topic```](https://lb.yandex-team.ru/logbroker/accounts/market-mbo/test/deepmind/offer-hidings-topic)
    - Production [```market-mbo/prod/deepmind/offer-hidings-topic```](https://lb.yandex-team.ru/logbroker/accounts/market-mbo/prod/deepmind/offer-hidings-topic)

- ```market-indexer/*/blue/stock-storage```

    - Назначение: Топик с информацией о стоках
    - Формат: ```Market::DataCamp::SyncAPI::ChangeOfferRequest```
    - Поставщики: ```Stock-Storage```
    - Потребители: ```piper```
    - Testing [```market-indexer/testing/blue/stock-storage```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/blue/stock-storage)
    - Production [```market-indexer/prod/blue/stock-storage```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/stock-storage)

- ```market-indexer/*/blue/datacamp-offers```

    - Содержит сериализованные офера в формате [DatacampOffer](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto)
    - Поставщики: ```blue/miner, blue/stroller```
    - Потребители: ```piper```
    - Testing [```market-indexer/testing/blue/datacamp-offers```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/blue/datacamp-offers)
    - Production [```market-indexer/prod/blue/datacamp-offers```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-offers)

- ```market-indexer/*/blue/datacamp-qoffers```

    - Назначение: Результат парсинга офферов синим qparser
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```blue/qparser```
    - Потребители: ```piper```
    - Testing [```market-indexer/testing/blue/datacamp-qoffers```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/blue/datacamp-qoffers)
    - Production [```market-indexer/prod/blue/datacamp-qoffers```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-qoffers)

- ```market-indexer/*/blue/datacamp-messages```

    - Содержит сериализованные офера в формате [DatacampMessage](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/DatacampMessage.proto)
    - Поставщиком данных является [blue/push-parser](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/parser) и [blue/qparser](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/feeds/qparser)
    - Потребители: ```piper```
    - Testing [```market-indexer/testing/blue/datacamp-messages```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/blue/datacamp-messages)
    - Production [```market-indexer/prod/blue/datacamp-messages```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-messages)

- ```market-indexer/*/white/datacamp-offers-blog```

    - Назначение: Содержит вспомогательную информацию об офере(ошибки обработки, ...)
    - Формат: ```OfferBlog```
    - Поставщики: ```white/push-parser, piper, white/miner, scanner, white/stroller```
    - Потребители: ```piper```
    - Testing [```market-indexer/testing/white/datacamp-offers-blog```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/white/datacamp-offers-blog)
    - Production [```market-indexer/prod/white/datacamp-offers-blog```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/white/datacamp-offers-blog)

- ```market-indexer/*/white/datacamp-messages```

    - Назначение:
        - Технические команды ```Market::DataCamp::DatacampMessage::tech_command``` от ```white/push-parser```
        - united-офферы ```Market::DataCamp::DatacampMessage::united_offers``` после майнинга через ```united/miner```
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```united/miner, white/push-parser```
    - Потребители: ```piper```
    - Testing [```market-indexer/testing/white/datacamp-messages```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/white/datacamp-messages)
    - Production [```market-indexer/prod/white/datacamp-messages```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/white/datacamp-messages)

- ```market-indexer/*/united/datacamp-offers-from-miner```

    - Назначение: united-офферы, после майнинга
    - Формат: ```Market::DataCamp::DatacampMessage::united_offers```
    - Поставщики: ```miner```
    - Потребители: ```piper```
    - Testing [```market-indexer/testing/united/datacamp-offers-from-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-offers-from-miner)
    - Production [```market-indexer/prod/united/datacamp-offers-from-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-from-miner)

- ```market-indexer/*/united/datacamp-offers-from-routines```

    - Назначение: united-офферы из routines (периодические задачи: мигратор, удалятор, копир и пр.)
    - Формат: ```Market::DataCamp::DatacampMessage::united_offers```
    - Поставщики: ```routines```
    - Потребители: ```piper```
    - Testing [```market-indexer/testing/united/datacamp-offers-from-routines```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-offers-from-routines)
    - Production [```market-indexer/prod/united/datacamp-offers-from-routines```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-from-routines)

- ```mbi/*/assortment-market-quick```
    - Назначение: для изменения и создания информации о предложении клиента (MARKETINDEXER-37318)
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```MBI```
    - Потребители: ```piper```
    - Testing [```mbi/test/assortment-market-quick```](https://lb.yandex-team.ru/logbroker/accounts/mbi/test/assortment-market-quick)
    - Production [```mbi/prod/assortment-market-quick```](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/assortment-market-quick)

- ```mbi/*/internal-market-quick```
    - Назначение: Топик со скрытиями/ценами от MBI (маркетные==internal скрытия) MARKETINDEXER-38391
        - На момент создания apr-2021 передаются скрытия для синих офферов из-за превышения цены (исторически расчет в MBI)
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```MBI```
    - Потребители: ```piper```
    - Testing [```mbi/test/internal-market-quick```](https://lb.yandex-team.ru/logbroker/accounts/mbi/test/internal-market-quick)
    - Production [```mbi/prod/internal-market-quick```](https://lb.yandex-team.ru/logbroker/accounts/mbi/prod/internal-market-quick)

- ```market-mbo/*/datacamp/datacamp-render-model```
    - Назначение: Топик с карточками моделей (msku) от MDM MARKETINDEXER-38020.
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```MDM```
    - Потребители: ```piper```
    - Testing [```market-mbo/test/datacamp/datacamp-render-model```](https://lb.yandex-team.ru/logbroker/accounts/market-mbo/test/datacamp/datacamp-render-model)
    - Production [```market-mbo/prod/datacamp/datacamp-render-model```](https://lb.yandex-team.ru/logbroker/accounts/market-mbo/prod/datacamp/datacamp-render-model)

- ```market-indexer/*/united/datacamp-offers-from-msku-miner```
    - Назначение: Топик с обновлениями карготипов в оффере через быстрый пайплайн
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```msku_miner```
    - Потребители: ```piper```
    - Testing [```market-indexer/testing/united/datacamp-offers-from-msku-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-offers-from-msku-miner)
    - Production [```market-indexer/prod/united/datacamp-offers-from-msku-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-from-msku-miner)

## Выходные топики
- ```market-indexer/*/united/datacamp-subscription-messages```
    - Назначение: Внутренний топик хранилища для отправки данных об изменении оферов
    - Формат: ```Market::DataCamp::UnitedOffersSubscriptionMessage```
    - Поставщики: ```Datacamp Controllers```
    - Потребители: ```Datacamp Dispatcher```
    - Testing [```market-indexer/testing/united/datacamp-subscription-messages```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-subscription-messages)
    - Production [```market-indexer/prod/united/datacamp-subscription-messages```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-subscription-messages)

- ```market-partner-status/*/datacamp-offer-updates```
    - Назначение: Информирование MBI о появлении новых офферов в ОХ
    - Формат: ```Market::DataCamp::DatacampMessage```
    - Поставщики: ```piper```
    - Потребители: ```MBI```
    - Testing [```market-partner-status/test/datacamp-offers-updates```](https://logbroker.yandex-team.ru/logbroker/accounts/market-partner-status/test/datacamp-offer-updates)
    - Production [```market-partner-status/prod/datacamp-offers-updates```](https://logbroker.yandex-team.ru/logbroker/accounts/market-partner-status/prod/datacamp-offer-updates)

- ```mbi/*/datacamp-ff4shops-offers-changes```
    - Назначение: Экспорт в mbi [(сервис ff4shops)](https://abc.yandex-team.ru/services/ff4shops/) данных о появлении новых офферов в ОХ, изменении approved-маппингов, архивного статуса и статуса публикации
    - Формат: ```Market::DataCamp::Offer```
    - Поставщики: ```piper```
    - Потребители: ``ff4shops```
    - Testing [```mbi/test/datacamp-ff4shops-offers-changes```](https://logbroker.yandex-team.ru/logbroker/accounts/mbi/test/datacamp-ff4shops-offers-changes)
    - Production [```mbi/prod/datacamp-ff4shops-offers-changes```](https://logbroker.yandex-team.ru/logbroker/accounts/mbi/prod/datacamp-ff4shops-offers-changes)

- ```market-mbo/*/datacamp/datacamp-fast-mappings```
    - Назначение: Экспорт в маппингов в MBO [(сервис content-storage)](https://abc.yandex-team.ru/services/content_storage_fast_mappings/) данных об изменении маппингов
    - Формат: ```Market::DataCamp::EnrichedOffer```
    - Поставщики: ```piper```
    - Потребители: ``content-storage-fast-mappings```
    - Testing [```market-mbo/test/datacamp/datacamp-fast-mappings```](https://lb.yandex-team.ru/logbroker/accounts/market-mbo/test/datacamp/datacamp-fast-mappings)
    - Production [```market-mbo/prod/datacamp/datacamp-fast-mappings```](https://lb.yandex-team.ru/logbroker/accounts/market-mbo/prod/datacamp/datacamp-fast-mappings)
