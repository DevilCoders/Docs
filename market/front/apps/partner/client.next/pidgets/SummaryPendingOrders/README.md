# SummaryPendingOrders (Заказы, требующие подтверждения)

<img src="https://media.github.yandex-team.ru/user/11807/files/d3f64800-e015-11eb-9741-affc7cbf84d5" width="300">

## Общее описание

Виджет, показывающий, у скольки заказов истекает срок доставки.
Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx))

| Права               | Поля из AppState | Модели | Фичи кокона |
| ------------------- | ---------------- | ------ | ----------- |
| Доступен всем ролям | `campaignId`     | DBS    | -           |

## Используемые бэкенды

Отправляется запрос на сводку по заказам магазина, берётся сумма неподтверждённых (`pending` + `pendingLast` из ответа ручки)

[getPartnerSummaryInfoUsingGET](http://mbi-partner.tst.vs.market.yandex.net:38271/swagger-ui.html#/partner-summary-controller/getPartnerSummaryInfoUsingGET)
