# TaskOnboardingSurvey (Опрос после прохождения подключения)

## Общее описание

Виджет, показывающий, сколько заказов без подтвержденой даты доставки. Используется в карусели активных задач на сводке.

| Права               | Поля из AppState | Модели | Фичи кокона |
| ------------------- | ---------------- | ------ | ----------- |
| Доступен всем ролям | `campaignId`,    | DBS    | -           |

## Используемые бэкенды

Отправляется запрос на список заказов, для которых еще не подтверждена дата доставки.

[getOrdersCountUsingGET](http://checkouter.tst.vs.market.yandex.net:39001/swagger-ui.html#/order-controller/getOrdersCountUsingGET)
