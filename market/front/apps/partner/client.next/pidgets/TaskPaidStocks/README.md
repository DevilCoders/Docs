# TaskPaidStocks (Задача товаров на платном хранении)

<img src="https://media.github.yandex-team.ru/user/7930/files/c24d9a00-a931-11ec-97b2-4bb4d3692e0c" width="300">

## Общее описание

Виджет, показывающий, сколько товаров находится на платном хранении на складах Яндекса. Если за хранение начислено в текущем периоде, то отображается также сумма к оплате. Используется в карусели активных задач на сводке

| Права               | Поля из AppState | Модели    | Фичи кокона |
| ------------------- | ---------------- | --------- | ----------- |
| Доступен всем ролям | `campaignId`     | FBY, FBY+ | -           |

## Используемые бэкенды

[getStockStorageSummaryInfoUsingGET](http://mbi-partner.tst.vs.market.yandex.net/swagger-ui.html#/supplier-summary-controller/getStockStorageSummaryInfoUsingGET)
