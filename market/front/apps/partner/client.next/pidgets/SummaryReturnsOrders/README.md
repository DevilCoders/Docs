# SummaryReturnsOrders (Невыкупленные заказы)

<img src="https://media.github.yandex-team.ru/user/7930/files/14af0480-efb7-11eb-9104-2586c5ad1fcc" width="600">

## Общее описание

Виджет, показывающий, сколько невыкупленных заказов будет выдано при высозе с СЦ. Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx))

| Права               | Поля из AppState | Модели | Фичи кокона |
| ------------------- | ---------------- | ------ | ----------- |
| Доступен всем ролям | `campaignId`,    | FBS    | -           |

## Используемые бэкенды

Отправляется запрос на список заказов из которого забираем информацию о невыкупах

[getOrderSummaryInfoV2UsingGET](http://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/supplier-summary-controller/getOrderSummaryInfoV2UsingGET)
