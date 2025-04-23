# paymentReportYtGeneratorExecutor

### Код

[джоба paymentReportYtGeneratorExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/report/payment/PaymentReportYtGeneratorExecutor.java)


### Роль в работе продукта/подсистемы

Поставка данных для отчета о платежах.


### Датафлоу

Читает из

//home/market/production/billing/dictionaries/accrual
//home/market/production/billing/dictionaries/accrual_correction/latest
//home/market/production/billing/dictionaries/payout_group_payment_order/latest
//home/market/production/billing/dictionaries/payout/latest
//home/market/production/billing/dictionaries/payout_correction/latest
//home/market/production/mstat/dictionaries/mbi_bank_order/latest
//home/market/production/mstat/dictionaries/mbi_bank_order_item/latest
//home/market/production/mbi/billing/oracle-export-tm/market_billing_cpa_order
//home/market/production/mbi/billing/oracle-export-tm/market_billing_cpa_order_item
//home/market/production/mbi/dictionaries/partner_contract/latest
//home/market/production/mstat/oebs/sales_daily_market
//home/market/production/mbi/reports/old_trust_transaction
//home/market/production/mbi/reports/trust_transaction

Пишет в
//home/market/production/mbi/reports/agg_payment_report


### Способы наблюдения за текущим состоянием

- Juggler-проверки:
  tms-18


### Какая функциональность пострадает от отказа джобы
Построение отчета о платежах



### Как пользователи (или команда) заметят проблему и через какое время
Поддержка b2b при закрытии месяца



### Контакты разработчиков и менеджеров

Разработчики: [Группа продуктовой разработки Биллинга Маркета](https://staff.yandex-team.ru/departments/yandex_monetize_market_marketdev_business_billing_dev_dep62586/) <br/>
Менеджеры: [login](https://staff.yandex-team.ru/)

### Желательное время исправления в случае поломки
24 часа



### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни

