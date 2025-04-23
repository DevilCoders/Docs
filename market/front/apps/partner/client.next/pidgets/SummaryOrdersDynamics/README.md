# SummaryOrdersDynamics (Динамика заказов)

<img src="https://media.github.yandex-team.ru/user/11807/files/5e36b000-e006-11eb-958a-8ad902b336a4" width="400">

## Общее описание

Показывает данные по заказам и выручке за периоды неделя, две недели, текущий месяц, прошлый месяц в виде графика. Если данных за период нет, показывается пустое окно с 0 заказов.
Используется на единой сводке магазинов ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx)) и маркетплейса ([client.next/pages/MarketplaceSummary/App.tsx](/client.next/pages/MarketplaceSummary/App.tsx))

| Права         | Поля из AppState            | Модели             | Фичи кокона                 |
| ------------- | --------------------------- | ------------------ | --------------------------- |
| Доступен всем | `businessId` и `campaignId` | FBX, DBS, BUSINESS | `canViewProceeds`, isNewbie |

## Используемые бекенды

### MBI-Order-Service

#### На сводке магазина
[getDeliveredOrderForPartnerSummaryByDate](http://mbi-order-service.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/order-service-api.yaml#/partnerSummary/getDeliveredOrderForPartnerSummaryByDate)

#### На сводке маркетплейса
[getDeliveredOrderForBusinessSummaryByDate](http://mbi-order-service.tst.vs.market.yandex.net/swagger-ui/index.html?url=/openapi/order-service-api.yaml#/businessSummary/getDeliveredOrderForBusinessSummaryByDate)

## Пропсы

```
import type {Period} from 'shared/types/mbiOrderService/OrdersStat';

export type Props = {
    canShowMoney: boolean;
    period: Period;
    useInBusiness: boolean;
};
```

`canShowMoney`- виджет показывает графики выручки и заказов при `true`,
при `false` - только график заказов

`period`- выбранный период. Один из `WEEK`, `TWO_WEEKS`, `MONTH`, `PREV_MONTH`

`useInBusiness`- выводить дынные по бизнесу или магазину. Важно: если `useInBusiness = true` на странице должен быть `businessId` или `useInBusiness = false` то должен быть `campaignId`

## Особенности работы виджета

Просмотр выручки, как и графика с выручкой, доступен пользователям с ролями `PARTNER_READER` и `SHOP_ADMIN` из кокона. Наличие прав должно определять значение пропса `canShowMoney`. Пример:

```
export const UnitedSummary = (): ReactElement => {
    const canShowMoney = useSelector(makeIsFeatureAllowed('canViewProceeds'));

    ...

    return <SummaryOrdersDynamics canShowMoney={canShowMoney} />;
}
```

см. фичу кокона [canViewProceeds](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/cocon/cabinet-configs/src/main/resources/cabinets/shop.json) и её использование в коде.

## Моки (так было... сейчас токого нет, но хотелось бы сделать)

Реальные данные на бекенде доступны только в продакшен окружениях, поэтому при разработке и на тестовых стендах виджеты будут в «пустом» состоянии. Для того, чтобы виджет отобразился с данными, можно воспользоваться query-параметром `mocked=true`. На виджете появится соответствующая плашка, что данные тестовые.
