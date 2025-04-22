# Как поддержать новый способ оплаты в Биллинге Маркета

## Теория

Каждый способ оплаты заказов (даже если он будет только для товаров 1p поставщика) должен быть поддержан в Биллинге Маркета. Иначе Маркет может показывать некорректную публичную отчетность, а также магазины не получат деньги за свои проданные товары.

Примеры существующих способов оплаты: предоплата (карта, Apple Pay, Google Pay, СБП), субсидийный платеж, постоплата, Тинькофф кредит, рассрочка, BNPL.

{% note info %}

При добавлении нового способа оплаты надо поддержать для него платежи и рефанды.

{% endnote %}

## Чеклист

1. Подготовить дизайн новых платежей и рефандов в чекаутере:
    * какие будут [PaymentGoal](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L16)
      и [PaymentMethod](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentMethod.java?rev=r9734999#L26)
    * будут ли виртуальные платежи (например, как для BNPL - [`VIRTUAL_BNPL`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L115))
    * какие будут чеки, их количество
    * как будут работать рефанды
    * будут ли [{#T}](payment-control-ext.md#613-refandy)
2. Доработать [{#T}](payment-contract.md) между Чекаутером и Биллингом Маркета: подробно на примере существующих способов оплаты написать, как будет работать новый способ оплаты.
3. Провести встречу с Чекаутером и Биллингом Маркета: обсудить дизайн нового способа оплаты и зафиксировать контракты в тикете [MARKETCHECKOUT-22935](https://st.yandex-team.ru/MARKETCHECKOUT-22935) новым комментарием.
4. Обсудить с yaroshenko@ продуктовые требования к начислениям и выплатам: требуется ли их создавать, если да, то по какому сервису (610 или 609), с какими
   [product](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/payment/ProductType.kt?rev=r9196393#L9) и
   [paysys_type_cc](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/payment/PaysysTypeCc.kt?rev=r9431779#L9)
   сохранять их в тлоги. Предварительно завести в Балансе и OEBS
   [product](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/payment/ProductType.kt?rev=r9196393#L9) и
   [paysys_type_cc](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/payment/PaysysTypeCc.kt?rev=r9431779#L9).
6. Доработать GOE (в старом и новом компоненте): сохранение платежей, рефандов, чеков, создание accrual_trantime, order_payout_trantime, refund_payout_trantime.
7. Доработать джобы: в старом компоненте accrualMoneyFlowProcessingExecutor, payoutMoneyFlowProcessingExecutor, refundMoneyFlowProcessingExecutor, в новом компоненте domesticPayoutFromAccrualExecutor.
8. Обсудить с yaroshenko@, требуется ли биллить АВ для данного способа оплаты. Если хотим, то поддержать в биллинге АВ (биллинг, отчет по Услугам Маркетплейса, мониторинги).
9. Обсудить с tatkovalenko@, требуется ли отображать новый способ оплаты в отчетах ПИ (Заказы, Отчет по реализации). Если требуется, то доработать отчеты.
10. Добавить новый способ оплаты в сверки УВ между Чекаутером и Биллингом Маркета.
11. Проверить на проде, что для платежа и рефанда вся логика, указанная выше, работает корректно. Без данного пункта добавление нового способа оплаты не следует считать завершенным - есть риск что-то забыть, и узнать об этом слишком поздно.
