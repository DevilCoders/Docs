# Название джобы
globalOrderFeeBillingExecutor
### Код

[globalOrderFeeBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/globalOrderFeeBillingExecutor.java?rev=c518a63fca#L13)

### Продукт/подсистема
Доставка международных заказов (пока что Израиль)

### Роль в работе продукта/подсистемы

Берет трантаймы по международным заказам и биллит по статическим [тарифам](https://wiki.yandex-team.ru/users/marilukina/global-market/Commerce/#rates)

### Датафлоу

Берем за выбранную дату записи по трантаймам:
- `market_billing.global_order_trantime`
или
проверяем в таблице контрактов партнеров в команде перебилливания:
- `market_billing.global_partner_contract`


Считаем комиссию доставки в DTO [GlobalOrderDeliveryBilledAmount](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/order/model/GlobalOrderDeliveryBilledAmount.java?rev=c518a63fca#L19)

Кладем в таблицы с обиллеными значениями:
- `market_billing.global_order_billed_amount`

### Способы наблюдения за текущим состоянием

TBA

### Какая функциональность пострадает от отказа джобы

Перестанем биллить эквайринг для международных заказов.

### Как пользователи (или команда) заметят проблему и через какое время

Увидим по падению джобы `globalOrderFeeBillingExecutor` или по пустым записям обилленой услуги `global_delivery`.

### Контакты разработчиков и менеджеров

Разработчики:
[Андрей Колчанов](https://staff.yandex-team.ru/a-kolchanov) <br/>
[Павел Репин](https://staff.yandex-team.ru/pavel-repin) <br/>
[Азат Джаныбеков](https://staff.yandex-team.ru/adjanybekov) <br/>
[Андрей Иванов](https://staff.yandex-team.ru/prof) <br/>
Менеджеры:
[Сергей Ярошенко](https://staff.yandex-team.ru/yaroshenko) <br/>
[Мария Штох](https://staff.yandex-team.ru/mashtoh) <br/>

### Желательное время исправления в случае поломки

ASAP, но в целом как и любой серви 612 - важно починить и пересчитать до конца месяца.

### Способы регулирования работы джобы

Можно исправить расписание или пересчитать с помощью команды в tms [recalculate-global-fee-billing](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/fulfillment/orders/GlobalOrderFeeBillingCommand.java?rev=c518a63fca#L18)

### Известные причины поломок
TBA

### Дополнительно: тонкости и подводные камни
TBA
