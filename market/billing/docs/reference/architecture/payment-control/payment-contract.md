# Контракт платежей, рефандов и чеков

Тикет с контрактом по событиям между Чекаутером и Маркет Биллингом: [MARKETCHECKOUT-22935](https://st.yandex-team.ru/MARKETCHECKOUT-22935)

Хорошо бы тоже добавить контекста - что за события такие, куда смотреть

Есть 2 вида событий по заказу, которые обрабатываются в Управлении выплатами.

## 1. События платежей, рефандов, чеков, финальное событие по заказу

### 1.1. События новых платежей и рефандов

Такие, как [`NEW_SUBSIDY`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L85),
[`NEW_CASH_PAYMENT`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L141),
[`NEW_PAYMENT`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L53),
[`NEW_VIRTUAL_PAYMENT`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L360),
[`REFUND`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L61),
[`SUBSIDY_REFUND`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L93),
[`CASH_REFUND`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L253),
[`TINKOFF_CREDIT_CASH_REFUND`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L345),
[`NEW_SURCHARGE_PAYMENT`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L402),
[`SURCHARGE_REFUND`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L410)
— на них Маркет Биллинг ходит в Чекаутер за платежами и рефандами.

### 1.2. События по чекам

Такие, как
[`RECEIPT_PRINTED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L117),
[`RECEIPT_GENERATED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L176),
[`CASH_REFUND_RECEIPT_PRINTED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L258)
— на них Маркет Биллинг ходит в Чекаутер за чеками.

### ~~1.3. Финальное событие по заказу: [`ALL_PAYMENTS_CREATED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L378)~~

{% note info %}

*В настоящее время в логике работы не используется*

{% endnote %}

~~Создается для каждого заказа в мультизаказе, означает, что для заказа были созданы все платежи, кроме [`SURCHARGE`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L145)
. Гарантируется, что после этого события новых платежей создаваться не будет, и гарантируется, что событие [`ALL_PAYMENTS_CREATED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L378)
придет позже остальных событий по созданию платежа (таких, как
[`NEW_SUBSIDY`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L85),
[`NEW_CASH_PAYMENT`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L141),
[`NEW_PAYMENT`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L53),
), кроме [`SURCHARGE`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L145)
. Иными словами, [`SURCHARGE`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L145)
-платеж может быть создан когда угодно.~~

## 2. Финальные события по платежу или рефанду, гарантирующие, что статус и суммы в платеже или рефанде уже не изменятся

### 2.1. Платежи

#### 2.1.1. [`ORDER_PREPAY`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L24), [`ORDER_POSTPAY`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L40), [`TINKOFF_CREDIT`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L102), [`VIRTUAL_BNPL`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L115), [`SURCHARGE`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L145), [`ORDER_ACCOUNT_PAYMENT`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L138)

Для данных платежей Чекаутер создает событие [`PAYMENT_CLEARED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L374)
, которое гарантирует, что:
1) все изменения этого платежа
2) создание, изменение всех receipt для платежа
3) события для 1) и 2)

произошли до события [`PAYMENT_CLEARED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L374).

Не гарантируется печать чеков (printed), но гарантируется, что сами чеки существуют, не изменятся, и будут доступны в HTTP ручках.

Печать чеков при этом может зависнуть, это ок. Платить деньги по данному платежу все равно надо, это исключительная ситуация, которую потом будут допинывать руками.

На событие [`PAYMENT_CLEARED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L374)
Маркет Биллинг ещё раз идет в Чекаутер за чеками и создает `accrual_trantime`. Может существовать от одного до двух receipt, содержащих и доставку (если она есть), и товары.

#### 2.1.2. [`SUBSIDY`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L32)

Для данных платежей Маркет Биллинг идёт в Чекаутер за чеками и создает `accrual_trantime`, если пришло любое первое событие из списка:
[`RECEIPT_GENERATED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L176),
[`RECEIPT_PRINTED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L117),
[`CASH_REFUND_RECEIPT_PRINTED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L258)
. Может существовать только один receipt, содержащий и доставку (если она есть), и товары.

### 2.2. Рефанды

#### 2.2.1.
[`ORDER_PREPAY`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L24)
[`ORDER_POSTPAY`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L40),
[`TINKOFF_CREDIT`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L102),
[`VIRTUAL_BNPL`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L115),
[`SUBSIDY`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L32),
[`SURCHARGE`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L145),
[`ORDER_ACCOUNT_PAYMENT`](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentGoal.java?rev=r9734999#L138)

Для рефандов данных платежей Маркет Биллинг идёт в Чекаутер за чеками и создает `accrual_trantime`, если пришло любое первое событие из списка:
[`RECEIPT_GENERATED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L176),
[`RECEIPT_PRINTED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L117),
[`CASH_REFUND_RECEIPT_PRINTED`](https://a.yandex-team.ru/arcadia/market/checkout/checkouter-client/src/java/ru/yandex/market/checkout/checkouter/event/HistoryEventType.java?rev=r9734932#L258)
. Может существовать только один receipt, содержащий и доставку (если она есть), и товары.
