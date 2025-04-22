
## StockStorage
- [Чаты](https://wiki.yandex-team.ru/market/development/incident-routing/#fulfilmentmarketaff)
- [Лекция про архитектуру](https://wiki.yandex-team.ru/delivery/fulfilment/Lekcija-pro-arxitekturu/)

## Datacamp to SS

Топик логброкера: **market-indexer/prod/blue/datacamp-partner-stock** [prod](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/datacamp-partner-stock), [testing](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/blue/datacamp-partner-stock)

Подписчик [partner_stock_subscriber:](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/common/extension.proto?rev=8268697#L97)
```
optional ESubscribeType partner_stock_subscriber = 1701069;
```

Пример поиска оффера в логфеллер-логах: [yql](https://yql.yandex-team.ru/Operations/YUYAlwVK8HLJXqX6Z7IfIaxdlHfp6TUJ2SopywfL9pI=)

Таблица, в которой хранится вся информация по маркетным стокам в SS: [mstat-stock_sku](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/mstat/dictionaries/stock_sku/1d/latest)

## SS to Datacamp
SS шлет данные для хранилища в топик логброкера **market-indexer/prod/blue/stock-storage** [prod](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/prod/blue/stock-storage), [testing](https://lb.yandex-team.ru/logbroker/accounts/market-indexer/testing/blue/stock-storage)

Логфеллер-логи **stock-market-quick-log**: [prod](https://yt.yandex-team.ru/arnold/navigation?path=//logs/stock-market-quick-log), [test](https://yt.yandex-team.ru/arnold/navigation?path=//logs/stock-market-quick-log-testing)

Пример поиска оффера в логфеллер-логах: [yql](https://yql.yandex-team.ru/Operations/YUnrJtjKS5vGKvwXG8smh_TtfVRAjzExEsa8k5uFBKE=)
