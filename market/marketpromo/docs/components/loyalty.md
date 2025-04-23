# Лоялти

## Размазывание
Скидка распределяется, увеличивается в пользу пользователя.
Стоимость должна быть минимум 1р иначе акция не применится

## Порядок расчёта скидки { #calc }
1. external discount (DIRECT_DISCOUNT, BLUE_FLASH, PRICE_DROP_AS_YOU_SHOP)
2. комплекты (CHEAPEST_AS_GIFT, BLUE_SET, GIFT_WITH_PURCHASE)
3. Sorry купон (промокод) (COUPON)
4. spread discount (SPREAD_COUNT, SPREAD_RECEIPT)
5. промокоды и маркет купоны (COIN, PROMOCODE)
6. доставка

## Тех информация
Белый список выгружается на mds: http://market-loyalty.s3.mds.yandex.net/market-loyalty/free-delivery/loyalty_delivery_discount.pbuf.sn

Протобуф лоялти https://github.yandex-team.ru/market-java/market-loyalty/blob/master/market-loyalty-core/src/main/proto/LoyaltyFastPipeLine.proto

Протобуф репорт https://a.yandex-team.ru/arc/trunk/arcadia/market/proto/LoyaltyFastPipeLine.proto

Общее описание архитектуры https://wiki.yandex-team.ru/market/development/loyalty/arxitektura-quick-guide/
