# SummaryGoodsStatUnited (Товары для единого каталога )

## Общее описание

Используется на единой сводке магазинов **для нового каталога** ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx)).


| Права               | Поля из AppState | Модели   | Фичи кокона     |
| ------------------- | ---------------- | -------- | --------------- |
| Доступен всем ролям | `campaignId`     | FBX, DBS | isUnitedCatalog |


## Описание вкладки Товары
<img src="https://media.github.yandex-team.ru/user/11807/files/9f34c180-e012-11eb-9eb2-d1f1d7312182" width="300">

Виджет, показывающий общее количество товаров, а также доли отображаемых, скрытых товаров и товаров, по которым нужна информация.

При доле скрытых товаров больше 5% показывает жёлтое сообщение с призывом исправить проблемы (меняет цвет на красный при скрытиях от 45%).


## Используемые бэкенды

[getBusinessOfferIntegralStatusStatsUsingGET](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/business-summary-controller/getBusinessOfferIntegralStatusStatsUsingGET)
