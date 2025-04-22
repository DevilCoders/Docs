# SummaryAdvStrategiesAccount (Счет для рекламных стратегий)

<img src="https://media.github.yandex-team.ru/user/7930/files/b7675200-e32c-11eb-9800-aa8c9a090fae" width="300">

## Общее описание

Виджет, показывающий информация о состоянии счета для рекламных стратегий партнера. Также через него можно пополнить счет (отдельная модалка) и перейти к статистике по стратегиям ([client.next/pages/FulfillmentSummary/components/Content/index.tsx](/client.next/pages/FulfillmentSummary/components/Content/index.tsx))

| Права                                                       | Поля из AppState       | Модели  | Фичи кокона |
| ----------------------------------------------------------- | ---------------------- | ------- | ----------- |
| Доступен всем ролям (имеет ограничения на пополнение счета) | `campaignId`, `userId` | FBX/DBS | -           |

Доступность пополнения счета определяется фичей `hasWriteRights`. Для DBS также бункер-настройками `payment-dsbs`.

## Используемые бэкенды

-   получение финансовой информации: [getCampaignFinanceInfo](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-core/src/java/ru/yandex/market/core/billing/DbBillingService.java?rev=r8407371#L142)

-   получение овердрафта клиента: [getClientOverdraft](https://wiki.yandex-team.ru/MBI/NewDesign/components/market-payment/ruchki/clientOverdraft/)

-   получение бюджетных лимитов: [getPopularDatasourceParams](https://wiki.yandex-team.ru/mbi/newdesign/components/market-payment/getPopularDatasourceParams/)

-   получение настроек автопополнения счета: [getAutoPaymentSettings](https://a.yandex-team.ru/arc/trunk/arcadia/market/mbi/mbi/mbi-partner/src/java/ru/yandex/market/partner/mvc/controller/billing/AutoPaymentController.java?rev=r8407503#L83)
