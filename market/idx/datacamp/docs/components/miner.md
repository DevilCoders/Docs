# Miner (Микросервис переобогащения оферного хранилища)

Читает офера на переобогащения из топика [```market-indexer/prod/united/datacamp-offers-to-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-to-miner?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1621872445119&metricsTo=1621958845119&sortOrder=%22default%22)

После переобогащения пишет в выходной топик [```market-indexer/prod/united/datacamp-offers-from-miner```](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-from-miner?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1621872457746&metricsTo=1621958857746&sortOrder=%22default%22)

Посмотреть содержимое топиков можно через logfeller - [yql](https://yql.yandex-team.ru/Operations/YK0hNRJKfbwxF00AMOY_Vzo8S0jUC59TnzUruRCCKG8=)

## Регулярный майнинг

Таска рутин Routines.SenderToMiner регулярно отправляет офферы на перемайнинг в топик логброкера **market-indexer/*/united/datacamp-offers-to-miner-regular**
[prod](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-to-miner-regular), [testing](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-offers-to-miner-regular)

Офферы после перемайнинга отправляются в топик логброкера **market-indexer/*/united/datacamp-offers-from-miner-regular**
[prod](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/united/datacamp-offers-from-miner-regular), [testing](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-offers-from-miner-regular)

Пример поиска по логфеллеру: [yql](https://yql.yandex-team.ru/Operations/YrF6NtJwbCVQSaG2XOVlTAMYCd-bGar9bRFhtC1VrHI=)

## Запросы в УК (UltraController)

Miner отправляет [DataCampOffer](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/offer/DataCampOffer.proto#L41) на дообогащение в [UltraController](https://wiki.yandex-team.ru/market/development/datapreparation/ultracontroller/) и получает от него [EnrichedOffer](https://a.yandex-team.ru/arc/trunk/arcadia/market/proto/ir/UltraController.proto?rev=r8758231#L157), в котором содержится информация о матчинге на [msku](https://wiki.yandex-team.ru/users/antsa4/projects/msku/).

Запросы и ответы от УК можно отслеживать в топике [```market-indexer/prod/united/datacamp-uc-requests-from-miner-log```](https://logbroker.yandex-team.ru/logbroker/accounts/market-indexer/testing/united/datacamp-uc-requests-from-miner-log?page=statistics&type=topic&tab=writeMetrics&shownTopics=all%20topics&metricsFrom=1637665371095&metricsTo=1637751771095&sortOrder=%22default%22)

Для отладки походов в УК можно пользоваться выгрузкой [logfeller](https://yql.yandex-team.ru/Operations/YZ4dq9JwbConNy4klfDpq-8BTl_W6xUg1Lks9KSfyYY=).
Пример такого запроса: [найти обращения из miner в UC для заданных магазинов](https://yql.yandex-team.ru/Operations/YYvJAwVK8IhSJLxEg7a94f7m22BSmqbMmNrJv5fovOc=)
