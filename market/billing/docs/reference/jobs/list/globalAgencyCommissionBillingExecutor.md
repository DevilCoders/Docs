# Название джобы
globalAgencyCommissionBillingExecutor
### Код

[GlobalAgencyCommissionBillingExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/agency/commission/GlobalAgencyCommissionBillingExecutor.java#L13)

### Продукт/подсистема
Агентское Вознаграждение (АВ/эквайринг) международных заказов (пока что Израиль)

### Роль в работе продукта/подсистемы

Берет начисления по международным заказам и биллит по статическому тарифу (2.5%)

### Датафлоу

Берем за выбранную дату записи по начислениям и действующим контрактам из таблиц:
- `market_billing.accrual`
- `shops_web.supplier_contract`


Считаем комиссию эквайринга (АВ) в DTO [AgencyCommissionBilledAmount](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/agency/model/AgencyCommissionBilledAmount.java?rev=dc149f4542#L16)

Кладем в таблицы с обиллеными значениями:
- `market_billing.global_agency_comm_billed_amount`

### Способы наблюдения за текущим состоянием

TBA

### Какая функциональность пострадает от отказа джобы

Перестанем биллить эквайринг для международных заказов.

### Как пользователи (или команда) заметят проблему и через какое время

Увидим по падению джобы `globalAgencyCommissionBillingExecutor` или по пустым записям обилленой услуги `global_agency_commission`.

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

Можно исправить расписание или пересчитать с помощью команды в tms [recalculate-global-agency-commission-billing](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/agency/commission/GlobalAgencyCommissionBillingCommand.java#L18)

### Известные причины поломок
TBA

### Дополнительно: тонкости и подводные камни
TBA
