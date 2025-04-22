# SummaryOrdersDeprecated (Заказы)

> Этот компонент не нужно использовать, используйте SummaryOrders

<img src="https://media.github.yandex-team.ru/user/11807/files/3a726a80-e004-11eb-878b-288a3ec2c393" width="300">

## Общее описание

Показывает данные по заказам за последние 28 дней.
Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx)) и маркетплейса ([client.next/pages/MarketplaceSummary/App.tsx](/client.next/pages/MarketplaceSummary/App.tsx))

| Права               | Поля из AppState            | Модели | Фичи кокона |
| ------------------- | --------------------------- | ------ | ----------- |
| Доступен всем ролям | `businessId` и `campaignId` | DBS    | -           |

## Используемые бэкенды

[getOrdersSummaryUsingGET](https://mbi-partner-stat.tst.vs.market.yandex.net/swagger-ui.html#/shop-summary-controller/getOrdersSummaryUsingGET)

## Моки

Реальные данные на бекенде доступны только в продакшен окружениях, поэтому при разработке и на тестовых стендах виджеты будут в «пустом» состоянии. Для того, чтобы виджет отобразился с данными, можно воспользоваться query-параметром `mocked=true`. На виджете появится соответствующая плашка, что данные тестовые.
