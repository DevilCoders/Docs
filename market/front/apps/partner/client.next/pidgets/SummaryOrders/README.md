# SummaryOrders (Заказы)

<img src="https://media.github.yandex-team.ru/user/11807/files/3a726a80-e004-11eb-878b-288a3ec2c393" width="300">

## Общее описание

Показывает данные по заказам за периоды неделя, две недели, текущий месяц, прошлый месяц.
Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx)) и маркетплейса ([client.next/pages/MarketplaceSummary/App.tsx](/client.next/pages/MarketplaceSummary/App.tsx))

| Права               | Поля из AppState            | Модели | Фичи кокона |
| ------------------- | --------------------------- | ------ | ----------- |
| Доступен всем ролям | `businessId` и `campaignId` | DBS    | -           |

## Используемые бэкенды

### MBI-Order-Service

#### На сводке магазина
[getDeliveredOrderCountForPartnerSummary](http://mbi-order-service.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/order-service-api.yaml#/partnerSummary/getDeliveredOrderCountForPartnerSummary)

#### На сводке маркетплейса
[getDeliveredOrderCountForBusinessSummary](http://mbi-order-service.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/order-service-api.yaml#/businessSummary/getDeliveredOrderCountForBusinessSummary)

## Моки (так было... сейчас токого нет, но хотелось бы сделать)

Реальные данные на бекенде доступны только в продакшен окружениях, поэтому при разработке и на тестовых стендах виджеты будут в «пустом» состоянии. Для того, чтобы виджет отобразился с данными, можно воспользоваться query-параметром `mocked=true`. На виджете появится соответствующая плашка, что данные тестовые.
