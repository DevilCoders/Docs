# SummaryCustomerCommunication (Общение с клиентами)

<img src="https://media.github.yandex-team.ru/user/11807/files/538d1280-e028-11eb-9b76-28e63aa0b84e" width="300">

## Общее описание

Виджет, показывающий количество чатов с клиентами и споров и содержащий кнопку перехода к чатам. Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx))

| Права               | Поля из AppState | Модели | Фичи кокона |
| ------------------- | ---------------- | ------ | ----------- |
| Доступен всем ролям | `campaignId`     | DBS    | -           |

## Используемые бэкенды

-   для количества споров и неотвеченных запросов: [getPartnerConsultationsStatistics](https://a.yandex-team.ru/arc_vcs/market/lilucrm/ocrm/module_order_arbitrage/src/main/java/ru/yandex/market/ocrm/module/order/arbitrage/controller/ArbitrageController.java?rev=e4f8331613990a4055c69c3db79331080488ec4b#L135)

-   для количества чатов: [getPartnerShopQuestionsByModelsUsingPOST](http://pers-qa.tst.vs.market.yandex.net/swagger-ui.html#/partner-shop-controller/getPartnerShopQuestionsByModelsUsingPOST)
