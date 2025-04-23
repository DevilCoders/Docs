
## Вопросы про офферное хранилище
1. Начните с самостоятельного поиска ответа на свой вопрос по этой документации, wiki, стартреку.
1. При наличии ошибки [заведите тикет в очереди индексатора](https://st.yandex-team.ru/createTicket?queue=MARKETINDEXER), опишите проблему и способ воспроизведения. Обязательно укажите идентификаторы магазина (business_id, shop_id), фида (datafeed_id), оффера (offer_id). Тикет будет разобран саппортом в порядке выданного приоритета.
1. [Хотлайн чат индексатора](https://t.me/joinchat/BD4-z0bMfQ7alBC3Bfyfxg) для связи с дежурными или координатором. В этом же чате задаются вопросы по работе хранилища и разработке.

## Посмотреть содержимое фида

Использовать [архив фидов](../market/idx/datacamp/parser/README#feed_archives) индексатора.

## Проверить цены оффера

Для синих поставщиков весь поток партнерских данных идет через офферное хранилище, включая цены.
Цены могут быть установлены через фид, PAPI, партнерский интерфейс.

Точкой входа для расследования изменения цен является otrace:
```
http://active.idxapi.vs.market.yandex.net:29334/v1/otrace?feed=632362&offer=350212&date=20201111
```
- вместо ```20201111``` указать дату
- [подробнее про otrace](https://wiki.yandex-team.ru/market/support/expertberub2b/interfaces/otrace/)

По ссылке из otrace можно перейти в трассировку ЦУМ, где будут операции с синим оффером за сутки:
```
https://tsum.yandex-team.ru/trace/1605056400000/ee6cab04bf692d3291a28074115fc339
```

Также следует использовать [архив фидов](../market/idx/datacamp/parser/README#feed_archives).

Инструмент поиска по таблицам "дукалис" работает 10-15 минут и пишет отчет в тикет. Статус оффера текущий и исторический:
```
http://idxapi.vs.market.yandex.net:29334/v1/admin/dukalis/check_offer_status/
http://idxapi.vs.market.yandex.net:29334/v1/admin/dukalis/check_offer_history_price/
```
- [инструкция в коде](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/devtools/dukalis/README.md)


## Типы парсинга фидов в пуш-схеме

https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/api/UpdateTask.proto?blame=true&rev=r8200435#L81-97

Наиболее распространенные типы парсинга в Едином Каталоге:
FEED_CLASS_SELECTIVE_BASIC_PATCH_UPDATE_SERVICE_PATCH_UPDATE - "Обновить прайс-лист частично"
FEED_CLASS_SELECTIVE_BASIC_PATCH_UPDATE_SERVICE_FULL_COMPLETE - "Полностью заменить ассортимент"
FEED_CLASS_STOCK - стоковый фид
FEED_CLASS_ASSORTMENT_BASIC_PATCH_UPDATE_SALE_TERMS_SERVICE_FULL_COMPLETE - "Полностью заменить ассортимент, но обработка базовой и сервисной части происходит независимо"

Подробности: https://wiki.yandex-team.ru/market/development/indexer/arxitektura-marketnogo-indeksatora/offer-repository/newfeedtypes/

## Статус магазина в таблице partners

Статус магазина disabled, в случае если
 * присутствует решетка перед shop_id (#shop_id) либо is_enabled=false
 * is_alive отсутствует либо is_alive=false

Флажок is_alive показывает, что магазин "живой": либо недавно был выключен, либо пытается включиться. Значение приходит от mbi. Доработка на стороне хранилища: [MARKETINDEXER-38794](https://st.yandex-team.ru/MARKETINDEXER-38794)

## Какой TVM для подключения
- Продакшн TVM: [2016907](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/etc/env/production.united?rev=8176659&blame=true#L133)
- Тестинг TVM: [2002296](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/etc/env/testing.united?rev=r8176659#L131)
- Продакшн consumer: [market-indexer/prod/white/datacamp-consumer-original](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/etc/env/production.united?rev=r8182716#L133)
- Тестинг consumer: [market-indexer/testing/white/datacamp-consumer-original](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/controllers/etc/env/testing.united?rev=r8182716#L131)
- [ABC сервис](https://abc.yandex-team.ru/services/datacamp/)

## Где лежат секреты сервисов хранилища
- [Testing](https://yav.yandex-team.ru/secret/sec-01dsfcej668h548vxvxgh8vw41/explore/versions)
- [Production](https://yav.yandex-team.ru/secret/sec-01dsfcm45eskn30121gqrb99zq/explore/versions)

## Вопросы про нормализацию оффера
Вопросы и ответы [здесь](../model/offers.md#normal)
