# WithdrawReminder (Виджет информирования о наличии собранных заявок на вывоз)

<img src="https://jing.yandex-team.ru/files/alantukh/Снимок%20экрана%202021-09-24%20в%2012.14.20.png" width="300">

## Общее описание

Виджет, отображаемый в случае, если у мерча есть собранные заявки на вывоз. Цель виджета - стимулировать мерча забрать товары по этим заявкам, когда он приедет на склад отгружать заказы / товары ([client.next/pages/FulfillmentSupplyCard/App.tsx](/client.next/pages/FulfillmentSupplyCard/App.tsx))

| Права               | Поля из AppState | Модели   | Фичи кокона |
| ------------------- | ---------------- | -------- | ----------- |
| Доступен всем ролям | `campaignId`     | FBY/FBY+ | -           |

## Используемые бэкенды

Отправляется запрос на получение списка заявок ffwf. Запрос отправляется только для определенного статуса заявки (REQUEST_STATUS.READY_TO_WITHDRAW), заявки запрашиваются только на вывоз.

[getRequestsUsingGET](http://ffw-api.tst.vs.market.yandex.net/swagger-ui.html#/request-controller/getRequestsUsingGET_1)
