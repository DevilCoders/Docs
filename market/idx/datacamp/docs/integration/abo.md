
## Cкрытия АБО

Cкрытия от АБО отправляются в топик логброкера 

* prod - [market-abo/production/hidden-offers](https://lb.yandex-team.ru/logbroker/accounts/market-abo/production/hidden-offers), поиск в логфеллер - [yql](https://yql.yandex-team.ru/Operations/YoydtJfFtyqtuNdhm0-492FNjN1m_2WeZoQcoV22jZU=)
* testing - [market-abo/testing/hidden-offers](https://lb.yandex-team.ru/logbroker/accounts/market-abo/testing/hidden-offers), поиск в логфеллер - [yql](https://yql.yandex-team.ru/Operations/YpC58gVK8Kmic0c4mJ7RGqWKmO7TYOpRsJZwmVjAhjI=)

Поддержано три вида скрытий для синих:

* **msku** - источник [**MARKET_ABO_MSKU**](https://a.yandex-team.ru/arcadia/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r9511352#L345)

* **msku + shop_id** - источник [**MARKET_ABO_MSKU_SHOP**](https://a.yandex-team.ru/arcadia/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r9511352#L346)

* **shop_id + shop_sku** - источник [**MARKET_ABO_SHOP_SKU**](https://a.yandex-team.ru/arcadia/market/idx/datacamp/proto/offer/OfferMeta.proto?rev=r9511352#L347)

В хранилище отправляется вердикт и скрытие с нужным источником. Вердикт с is_banned=true/false, скрытие с disabled=true/false (скрытие-раскрытие).

[Пример сообщения](https://paste.yandex-team.ru/9579146)

Также сканнер регулярно накатывает данные о скрытиях из таблицы:
[//home/market/production/abo/hiding_rule/blue_offer/recent](https://yt.yandex-team.ru/arnold/navigation?path=//home/market/production/abo/hiding_rule/blue_offer)

[Документация в АБО](https://wiki.yandex-team.ru/market/development/abo/hiding/logbroker/#belyeskrytija)
