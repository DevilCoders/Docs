# SummaryExpiringOrders (Заказы с истекающим сроком доставки)

<img src="https://media.github.yandex-team.ru/user/11807/files/9f818c80-e013-11eb-8fe4-58cb63748546" width="300">

## Общее описание

Виджет, показывающий, у скольки заказов истекает срок доставки. Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx))

| Права               | Поля из AppState              | Модели | Фичи кокона |
| ------------------- | ----------------------------- | ------ | ----------- |
| Доступен всем ролям | `campaignId`, `placementType` | DBS    | -           |

## Используемые бэкенды

Отправляется запрос на список заказов за последние X дней, для которых сегодня - последний день доставки. Из результата берётся только количество таких заказов

[getOrdersUsingGET](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/operations/order-controller/getOrdersUsingGET)
