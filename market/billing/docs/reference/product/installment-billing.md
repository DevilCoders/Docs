# Биллинг рассрочки

Мета тикет: [MARKETBILLING-419](https://st.yandex-team.ru/MARKETBILLING-419)

## Схема биллинга { #billing_schema }

![alt Схема биллинга](../../_assets/images/product/installment_billing_billing_schema.png "Схема биллинга" =900x300)

1. [INSTALLMENT](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/model/billing/BillingServiceType.java?rev=r9054246#L498) - Комиссия за оплату в рассрочку.
   - обилливаем услугу на статус delivery. Биллим товары в заказе с учетом субсидий (то есть по полной стоимости товара от партнера ДО применения субсидий/скидок/промо покупателем)
2. [INSTALLMENT_FINE](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/model/billing/BillingServiceType.java?rev=r9054246#L525) - Штраф за отмену заказа при оплате в рассрочку.
   - в случае, если магазин сам отменил заказ, оформленный в кредитную рассрочку (с переуступкой и без) между статусом proccessing и delivery - биллим услугу как штраф. В случае, если магазин отменил заказ между статусом delivery и delivered (характерно для DBS), то комиссию берем на delivery и не откатываем.
3. [INSTALLMENT_CANCALLATION](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/model/billing/BillingServiceType.java?rev=r9054246#L516) - Отмена комиссии за оплату в рассрочку.
   - если delivered не состоялся по причине отмены покупателя, невыкупа, отмены по вине СД, отмены по вине Маркета - не биллим или откатываем комиссию
4. [INSTALLMENT_RETURN_CANCELLATION](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/model/billing/BillingServiceType.java?rev=r9054246#L534) - Отмена комиссии при оплате в рассрочку при возврате товара.
   - если покупатель вернул товар (смотрим на дату перехода ретерна в REFUNDED) в течение 30 дней с момента перехода в статус delivery (момента обилливания) - откатываем комиссию по товару
5. если покупатель вернул товар (смотрим на дату перехода ретерна в REFUNDED) после 30 дней с момента перехода заказа в delivery - ничего не делаем
6. [INSTALLMENT_CANCELLATION](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/model/billing/BillingServiceType.java?rev=r9054246#L516) - Отмена комиссии за оплату в рассрочку.
   - если заказ переходит из статуса delivered в canceled, то откатываем комиссию по аналогии с fee
7. Тарифы:
    - 1,5 мес (bnpl) = 0%
    - 6 мес = 6% с 10 ноября
    - 12 мес = 12% с 10 ноября
    - 24 мес = 18% с 10 ноября

## Схема в бд { #database_common }

![alt Схема в бд 1](../../_assets/images/product/installment_billing_db_schema_1.png "Схема в бд 1" =900x500)
![alt Схема в бд 2](../../_assets/images/product/installment_billing_db_schema_2.png "Схема в бд 1" =350x350)

## Биллинг { #billing }

На текущий момент процесс биллинга размазан по двум компонентам: mbi и market_billing_tms.
В mbi биллятся услуги [InstallmentBillingService](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/mbi-billing/src/java/ru/yandex/market/billing/fulfillment/InstallmentBillingService.java?rev=r8948072#L51):
- [INSTALLMENT](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/model/billing/BillingServiceType.java?rev=r9054246#L498) - Комиссия за оплату в рассрочку.
- [INSTALLMENT_FINE](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/model/billing/BillingServiceType.java?rev=r9054246#L525) - Штраф за отмену заказа при оплате в рассрочку.
- [INSTALLMENT_CANCALLATION](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/model/billing/BillingServiceType.java?rev=r9054246#L516) - Отмена комиссии за оплату в рассрочку.

Обилленные значения попадают сразу как и в mbi, так и в market_billing_tms.

В market_billing_tms биллится услуга [InstallmentReturnBillingService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/installment/InstallmentReturnBillingService.kt?rev=r9181188#L29):
- [INSTALLMENT_RETURN_CANCELLATION](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/model/billing/BillingServiceType.java?rev=r9054246#L534) - Отмена комиссии при оплате в рассрочку при возврате товара.

Обилленные значения записываются только в market_billing_tms. В mbi, для отчетов, они попадают через выгрузки -
см. [Выгрузка и импорт обилленных значений возвратов](#return_export)

### Таблицы с обиленными значениями { #database_billing }

mbi
- [market_billing.installment_billed_amount](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/mbi-db/src/sql/market_billing/installment_billed_amount.sql?rev=r8860329#L4)
- [market_billing.installment_billed_amount_corr](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/mbi-db/src/sql/market_billing/installment_billed_amount_corr.sql?rev=r8860582#L7)
- [market_billing.installment_return_bill_amount](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/mbi-db/src/sql/market_billing/installment_return_bill_amount.sql?rev=r9170590#L4)

market_billing_tms
- [market_billing.installment_billed_amount](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/installment_billed_amount.sql?rev=r8890629#L4)
- [market_billing.installment_billed_amount_corr](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/installment_billed_amount_corr.sql?rev=r8890629#L7)
- [market_billing.installment_return_billed_amount](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/installment_return_billed_amount.sql?rev=r9182263#L5)

В тлог все собирается из market_billing_tms [InstallmentBilledAmountHelper](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/util/billing/InstallmentBilledAmountHelper.java?rev=r9181188#L29).
Отчеты строятся по mbi.

## Импорт возвратов { #return_import }

Возвраты импортируются двумя сервисами:
- [ImportOrderReturnsService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/ImportOrderReturnsService.java?rev=r9181188#L33) -
  таблица [market_billing.order_return](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/order_return.sql?rev=r9098737#L4)
- [ImportOrderReturnItemsService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/ImportOrderReturnItemsService.java?rev=r9181188#L24) -
  таблица [market_billing.order_return_item](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/order_return_item.sql?rev=r8924654#L4)

В момент импорта возврата создается трантайм [(ImportOrderReturnsService)](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/order/returns/ImportOrderReturnsService.java?rev=r9181188#L97) **только** для заказов рассрочки -
в таблице [market_billing.order_return_trantimes](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/order_return_trantimes.sql?rev=r9156058#L4).

Выгрузки для импорта в YT:
- testing
  - [//home/market/production/checkouter/testing/cdc/checkouter_main/return](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/market/production/checkouter/testing/cdc/checkouter_main/return)
  - [//home/market/production/checkouter/testing/cdc/checkouter_main/return_item](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/checkouter/testing/cdc/checkouter_main/return_item)
- production
  - [//home/market/production/checkouter/cdc/checkouter_main/return](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/market/production/checkouter/cdc/checkouter_main/return)
  - [//home/market/production/checkouter/cdc/checkouter_main/return_item](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/market/production/checkouter/cdc/checkouter_main/return_item)

## Выгрузка и импорт обилленных значений возвратов { #return_export }

Чтобы отобразить возвраты рассрочки в отчете Услуги маркетплейса, обиленные значения нужно импортировать в mbi.
Выгрузка осуществляется средствами mstat-а в разрезе дня - [ссылка на кофиг](https://a.yandex-team.ru/arc_vcs/market/mstat/components/dictionaries-yt/src/main/resources/configs/jdbc-dictionaries.yaml?rev=r9233781#L2765).

Выгрузки обиленных значений возвратов рассрочки:
- testing
  - [//home/market/testing/billing/dictionaries/installment/installment_return](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/market/testing/billing/dictionaries/installment/installment_return)
- production
  - [//home/market/production/billing/dictionaries/installment/installment_return](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/market/production/billing/dictionaries/installment/installment_return)

Сам импорт в mbi - [InstallmentReturnImportService](https://a.yandex-team.ru/arc_vcs/market/mbi/mbi/mbi-billing/src/java/ru/yandex/market/billing/installment/InstallmentReturnImportService.java?rev=r9244946#L21).

## Мониторинги {#monitoring}

Мониторинги по рассрочке в mbi включают в себя такие мониторы:
- все трантаймы до вчера обиллены
  - [Juggler - mbi-billing-3042](https://juggler.yandex-team.ru/check_details/?host=market_mbi_billing&service=mbi-billing-3042&project=market.common&query=&last=1DAY)
  - [документация](https://wiki.yandex-team.ru/mbi/development/monitoringssubs/3042/)
- по всем заказам с обилливаемым типом рассрочки есть трантаймы
  - [Juggler - mbi-billing-3043](https://juggler.yandex-team.ru/check_details/?host=market_mbi_billing&service=mbi-billing-3043&project=market.common&query=&last=1DAY)
  - [документация](https://wiki.yandex-team.ru/mbi/development/monitoringssubs/3043/)
- по всем отменам есть обилленые значения (равные сумме отмены по модулю)
  - [Juggler - mbi-billing-3044](https://juggler.yandex-team.ru/check_details/?host=market_mbi_billing&service=mbi-billing-3044&project=market.common&query=&last=1DAY)
  - [документация](https://wiki.yandex-team.ru/mbi/development/monitoringssubs/3044/)
- нет installment_cancellation и installment_fine одновременно
  - [Juggler - mbi-billing-3045](https://juggler.yandex-team.ru/check_details/?host=market_mbi_billing&service=mbi-billing-3045&project=market.common&query=&last=1DAY)
  - [документация](https://wiki.yandex-team.ru/mbi/development/monitoringssubs/3045/)
- нет одновременно записей installment/installment_fine
  - [Juggler - mbi-billing-3046](https://juggler.yandex-team.ru/check_details/?host=market_mbi_billing&service=mbi-billing-3046&project=market.common&query=&last=1DAY)
  - [документация](https://wiki.yandex-team.ru/mbi/development/monitoringssubs/3046/)

На мониторы возвратов (в market_billing_tms) одна ссылка в
[Juggler](https://juggler.yandex-team.ru/check_details/?host=market-billing&service=monitor-installment&project=market-billing&query=&last=1DAY)
- нет installment_return после 30 дней с момента доставки
- для всех installment_return есть обилленое значение без installment_cancellation
- installment_correction и installment_return не должны уйти в минус относительно обилленого значения

Так же в мониторингах на тлог в market_billing_tms добавлен блок с рассрочкой
- [market_billing.not_exported_tlog_collection](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/mon_tlog_collection.sql?rev=r9229687#L417)
- [market_billing.mon_tlog_consistency](https://a.yandex-team.ru/arc_vcs/market/billing/db/src/liquibase/market_billing/mon_tlog_consistency.sql?rev=r9229687#L632)
