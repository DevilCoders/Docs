Преобразовывает офферы фудтеха из [внешнего формата](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/proto/external/Offer.proto?rev=r8427067#L21) в united offer.

Логика обработки:
1. Офферы с общим business-id и offer-id, но разными shop-id, редьюсятся в один united.
2. TODO: офферы с shop_prices / shop_statuses разбиваются на сервисные офферы.
