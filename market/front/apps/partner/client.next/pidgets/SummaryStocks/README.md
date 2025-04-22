# SummaryStocks (Товары на платном хранении)

<img src="https://media.github.yandex-team.ru/user/11807/files/386dd300-e027-11eb-989d-afc72a729a65" width="300">

## Общее описание

Виджет, показывающий, сколько товаров находится на платном хранении на складах Яндекса. Если за хранение начислено в текущем периоде, то отображается также сумма к оплате.
Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx))

| Права               | Поля из AppState | Модели    | Фичи кокона |
| ------------------- | ---------------- | --------- | ----------- |
| Доступен всем ролям | `campaignId`     | FBY, FBY+ | -           |

## Используемые бэкенды

[getStockStorageSummaryInfoUsingGET](http://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/supplier-summary-controller/getStockStorageSummaryInfoUsingGET)
