# Управление выплатами и Факторинг

## Общее описание { #description }

Проект Управления Выплатами (УВ) и Факторинга возник из-за потребности гибкого управления выплатами денег мерчантам.
Например, возникла необходимость переводить деньги индивидуально для каждого мерчанта на определенные статусы заказа (УВ),
выплачивать один или два раза в месяц (Факторинг), совсем останавливать выплаты (Факторинг), использовать предварительный платеж (в будущем).

Для реализации вышеперечисленных возможностей, потребовалось добавить в систему Market-Billing-а такие понятия как [{#T}](#accrual) и [{#T}](#payout).

Итоговая схема (упрощенно) такая:
- Чекаутер кидает события по заказам: создание заказа, изменения статуса заказа, оплата, возврат, печать чека и т.п.
- Market-Billing слушает эти события и в нужный момент создает [{#T}](#accrual) и [{#T}](#payout)
- [{#T}](#accrual) как есть складываются в тлог (тут должна быть ссылка)
- [{#T}](#payout) группируются в [{#T}](#payment-order-draft) и в нужный момент еще раз гурппируются в [{#T}](#payment-order)
- [{#T}](#payment-order) складываются в тлог (тут должна быть ссылка)

## Глоссарий

### Начисления (Accrual) { #accrual }

обязательство Маркета перед мерчантом. Например, Маркет принял от пользователя 1000 рублей, и у него появляется обязательство эти 1000 рублей выплатить ему когда-нибудь в будущем. То же самое применимо к рефандам.

Появляется в момент перехода платежа в статус [CLEARED](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/pay/PaymentStatus.java?rev=r9734817#L42).

### Выплаты (Payout) { #payout }

переход обязательства ([{#T}](#accrual)) в реальную выплату. Есть требование учета, что выплата должна быть только после начисления (за исключением предварительного платежа).

Появляется в момент перехода заказа в статус [DELIVERED](https://a.yandex-team.ru/arcadia/market/checkout/checkout-common/src/java/ru/yandex/market/checkout/checkouter/order/OrderStatus.java?rev=r9734824#L35).

### Драфты команд на выплату (Payment Order Draft) { #payment-order-draft }

сгруппированные Маркет Биллингом [{#T}](#payout) в разрезе значимых полей (поставщик, контракт, тип оплаты и т.д.)

### Команды на выплату (Payment Order) { #payment-order }

сгруппированные Маркет Биллингом [{#T}](#payment-order-draft) в разрезе значимых полей (поставщик, контракт, тип оплаты и т.д.)

## Полезные ссылки:
* [основные потоки данных](payment-control-ext.md)
