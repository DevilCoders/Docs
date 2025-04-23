# SummaryDBSQualityAlert (Алерты на проблемы с качеством)

<img src="https://media.github.yandex-team.ru/user/11807/files/66dec300-e0a6-11eb-910a-59f1aa263e5a" width="400">

## Общее описание

Виджет, показывающий катоффы (отключения) и ограничения магазина. Эти катофы и ограничения должны повторять отображаемые на странице качества.
Отображается на единой сводке магазина ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx))


| Права                                                       | Поля из AppState               | Модели  | Фичи кокона |
| ----------------------------------------------------------- | ------------------------------ | ------- | ----------- |
| Доступен всем ролям (имеет ограничения на пополнение счета) | `campaignId` и `placementType` | DBS     | -           |


### Отображаемые катоффы

| Смысл катоффа                            | ID                          |
| ---------------------------------------- | --------------------------- |
| Размещение приостановлено вручную        | BY_PARTNER                  |
| Приостановлено из-за неактуальных данных | CART_DIFF                   |
| Магазин дублирует другой                 | CLONE                       |
| Подозрение в мошенничестве               | FRAUD                       |
| Непринятый заказ                         | ORDER_NOT_ACCEPTED          |
| Проблемы с качеством                     | OTHER                       |
| Прекратился обмен данными через api      | PINGER                      |
| Проблемы с качеством                     | QUALITY                     |
| Магазин на проверке                      | TESTING                     |
| Необходима проверка                      | QUALITY_MODERATION_REQUIRED |

Для отображения берётся первый попавшийся катоф.

[Список показываемых ограничений на сводке](https://wiki.yandex-team.ru/users/natalokshina/-stranica-kachestva-dsbs/#opisanieogranichenijj)

### Отображаемые ограничения

| Смысл ограничения                                            | ID                                    |
| ------------------------------------------------------------ | ------------------------------------- |
| по лицензии на продажу алкоголя                              | (type alco-offshops)                  |
| о точках, не отображающихся на карте                         | (type offshops)                       |
| нарушения правил в группах регионов                          | (type regionGroups)                   |
| нарушение гарантийного письма или правил размещения алкоголя | (feature-id 1006 ALCOHOL)             |
| уценённые товары скрыты                                      | (feature-id 1007 CUTPRICE)            |
| условия покупки в кредит скрыты из-за ошибок                 | (feature-id 1008 CREDITS)             |
| программа "маркетплейс" отключена                            | (feature-id 1009 MARKETPLACE_PARTNER) |
| логотип магазина не отображается                             | (feature-id 126 SHOP_LOGO)            |
| магазин не может продавать по акции                          | (feature-id 90 PROMO_CPC)             |
| нарушение правил продажи со скидками                         | (param DISCOUNTS_STATUS)              |

В первую очередь должны показываться ограничения на размещение со скидками, потом - по акции, а дальше - первое попавшееся ограничение. Сортировка - по полю `placement`, см. [RESTRICTION_FEATURES](/shared/resolvers/quality/restrictions/mapRestrictions.ts)

[Как формируются и отображаются ограничения](https://wiki.yandex-team.ru/market/market4shops/b2bcontour/contouronbording/dokumentacija-na-stranicu-kachestva/#sborifiltracijaogranichenijj)

### Особенности работы
- Ссылка "Подробнее", ведущая на страницу качества, не отображается для отключений, которые не относятся к качеству:
    - BY_PARTNER

## Используемые бекенжы

### Для катоффов

[getModerationShopProgramStatesUsingGET](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/moderation-controller/getModerationShopProgramStatesUsingGET)

Из ответа ручки берётся `ModerationShopProgramState.details.moderationCause` у первого попавшегося отключения

### Для ограничений

Ограничения собираются из нескольких источников.

Параметры кампании берутся в [getDatasourceParams](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/getDatasourceParams/).

Состояние участия магазина в программе (фичи) берётся из [featureInfo](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/featureInfo/).

Настройки доставки магазина берутся в [getDeliverySettingsAggregateData](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/getDeliverySettingsAggregateData/). Из них получаем группы регионов, не прошедшие проверку (`checkStatus === 'FAIL'`). Для каждой такой группы получаем статус проверки в [getStatusUsingGET](https://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/region-delivery-group-status-controller/getStatusUsingGET).

Информация по точкам продаж берётся в [showOutletSummary](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/showOutletSummary/).

Ограничение на количество заказов партнёра берётся в [ABO: getOrderLimitUsingGET](http://abo-public.tst.vs.market.yandex.net:38902/api/swagger-ui.html#/cpa-controller/getOrderLimitUsingGET)

Ответы ручек преобразуются в ограничения, как описано [здесь](https://wiki.yandex-team.ru/market/market4shops/b2bcontour/contouronbording/dokumentacija-na-stranicu-kachestva/#sborifiltracijaogranichenijj).
