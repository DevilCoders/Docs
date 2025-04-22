# TaskReturnOrders (Задача о невыкупленных заказах)

<img src="https://media.github.yandex-team.ru/user/7930/files/95998280-a931-11ec-829d-4d8526736b90" width="600">

## Общее описание

Виджет, показывающий, сколько невыкупленных заказов будет выдано при высозе с СЦ. Используется в карусели активных задач на сводке

| Права               | Поля из AppState | Модели | Фичи кокона |
| ------------------- | ---------------- | ------ | ----------- |
| Доступен всем ролям | `campaignId`,    | FBS    | -           |

## Используемые бэкенды

Отправляется запрос на список заказов из которого забираем информацию о невыкупах

[getOrderSummaryInfoV2UsingGET](http://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/supplier-summary-controller/getOrderSummaryInfoV2UsingGET)
