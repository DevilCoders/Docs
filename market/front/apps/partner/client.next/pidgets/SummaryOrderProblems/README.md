# SummaryOrderProblems («Невыкупы», «Возвраты», «Отмены»)

## Общее описание

Показывает данные о невыкупах, возвратах и отменах за периоды неделя, две недели, текущий месяц, прошлый месяц в виде графика 

| Права         | Поля из AppState            | Модели             |
| ------------- | --------------------------- | ------------------ |
| Доступен всем | `businessId` и `campaignId` | FBX, DBS, BUSINESS |

## Используемые бекенды

### MBI-Order-Service

#### На сводке магазина

[getProblemsOrderForPartnerSummaryByDate](http://mbi-order-service.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/order-service-api.yaml#/partnerProblemsSummary/getProblemsOrderForPartnerSummaryByDate)

#### На сводке маркетплейса

[getProblemsOrderForBusinessSummaryByDate](http://mbi-order-service.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/order-service-api.yaml#/businessProblemsSummary/getProblemsOrderForBusinessSummaryByDate)

## Пропсы

```
export type Props = {
    canShowMoney: boolean;
    useInBusiness: boolean;
};
```

`canShowMoney`- виджет показывает графики выручки и заказов при `true`,
при `false` - только график заказов

`useInBusiness`- выводить дынные по бизнесу или магазину. Важно: если `useInBusiness = true` на странице должен быть `businessId` или `useInBusiness = false` то должен быть `campaignId`

## Особенности работы виджета

Просмотр выручки, как и графика с выручкой, доступен пользователям с ролями `PARTNER_READER` и `SHOP_ADMIN` из кокона. Наличие прав должно определять значение пропса `canShowMoney`. Пример:

```
export const UnitedSummary = (): ReactElement => {
    const canShowMoney = useSelector(makeIsFeatureAllowed('canViewProceeds'));

    ...

    return <SummaryOrderProblems canShowMoney={canShowMoney} />;
}
```

см. фичу кокона [canViewProceeds](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/shop.json) и её использование в коде.
