# SummaryProceedDeprecated (Выручка)

> Этот компонент не нужно использовать, используйте SummaryProceed

<img src="https://media.github.yandex-team.ru/user/11807/files/e6617a80-df5e-11eb-905e-fdb045671ba6" width="300">

## Общее описание

Показывает выручку магазина или маркетплейса за 28 дней в рублях и процентное изменение по отношению к предыдущему периоду.
Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx)) и маркетплейса ([client.next/pages/MarketplaceSummary/App.tsx](/client.next/pages/MarketplaceSummary/App.tsx))

| Права                            | Поля из AppState            | Модели             | Фичи кокона       |
| -------------------------------- | --------------------------- | ------------------ | ----------------- |
| `PARTNER_READER` or `SHOP_ADMIN` | `businessId` и `campaignId` | FBX, DBS, BUSINESS | `canViewProceeds` |

## Используемые бэкенды

### Находясь на странице магазина (DBS/FBX):

[getRevenueSummaryUsingGET](https://mbi-partner-stat.tst.vs.market.yandex.net/swagger-ui.html#/shop-summary-controller/getRevenueSummaryUsingGET)

### Находясь на странице маркетплейса (BUSINESS):

[Swagger](???) // TODO добавить ссылку на доку по ручке для сводки маркетплейса

## Пропсы

```
export type Props = {
    canShowMoney: boolean;
};
```

`canShowMoney`- виджет показывает данные о выручке при `true`,
при `false` показывает сообщение о недостаточности прав

## Особенности работы виджета

Просмотр выручки, как и графика с выручкой, доступен пользователям с ролями `PARTNER_READER` и `SHOP_ADMIN` из кокона. Наличие прав должно определять значение пропса `canShowMoney`. Пример:

```
export const UnitedSummary = (): ReactElement => {
    const canShowMoney = useSelector(makeIsFeatureAllowed('canViewProceeds'));

    ...

    return <SummaryProceed canShowMoney={canShowMoney} />;
}
```

см. фичу кокона [canViewProceeds](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/shop.json) и её использование в коде.

## Моки

Реальные данные на бекенде доступны только в продакшен окружениях, поэтому при разработке и на тестовых стендах виджеты будут в «пустом» состоянии. Для того, чтобы виджет отобразился с данными, можно воспользоваться query-параметром `mocked=true`. На виджете появится соответствующая плашка, что данные тестовые.
