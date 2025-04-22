# PartnerGmvCalculationExecutor

### Код

[Тут](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/partner/gmv/PartnerGmvCalculationExecutor.java)


### Продукт/подсистема


Синий биллинг:агентские премии


### Роль в работе продукта/подсистемы

Считает GMV в разрезе партнёра для расчета агентских премий

### Датафлоу

Читает таблицы в PG: market_billing.cpa_order, cpa_order_item, cpa_order_status_history
Выгружает в market_billing.partner_gmv

### Способы наблюдения за текущим состоянием
Мониторингов пока нет, логи

### Какая функциональность пострадает от отказа джобы
Не будет информации о GMV партнёра, баланс не сможет посчитать агентские премии



### Как пользователи (или команда) заметят проблему и через какое время
Придут смежники, планируется мониторинг



### Контакты разработчиков и менеджеров

Разработчики: [phillippko](https://staff.yandex-team.ru/phillippko/)
Менеджеры: [k-sviridenko](https://staff.yandex-team.ru/k-sviridenko)


### Желательное время исправления в случае поломки
По возможности, до закрытия месяца

### Способы регулирования работы джобы
дата начала расчета - переменная в env market.billing.partner_gmv_calculation_executor.start_date


### Известные причины поломок




### Дополнительно: тонкости и подводные камни

