# SamplePidget (Пример ридми)

<img src="https://media.github.yandex-team.ru/user/11807/files/e6617a80-df5e-11eb-905e-fdb045671ba6" width="300">

## Общее описание

Виджет, существующий для примера, используется на [какой-нибудь странице](/client.next/pages/FulfillmentSummary/components/Content/index.tsx)

| Права               | Поля из AppState | Модели    | Фичи кокона |
| ------------------- | ---------------- | --------- | ----------- |
| Доступен всем ролям | `campaignId`     | FBY, FBY+ | -           |


## Используемые бэкенды

[getRevenueSummaryUsingGET](https://mbi-partner-stat.tst.vs.market.yandex.net/swagger-ui.html#/shop-summary-controller/getRevenueSummaryUsingGET)

## Пропсы

```
export type Props = {
    foo: string;
    bar: number;
};
```
