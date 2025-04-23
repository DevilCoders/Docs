# paymentReportYtExportExecutor

### Код

[джоба paymentReportYtExportExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/report/payment/PaymentReportYtExportExecutor.java)


### Роль в работе продукта/подсистемы

Выгружает в YT трастовые транзакции для отчета о платежах


### Датафлоу

Читает из

market_billing.cpa_order_transaction
market_billing.receipt_item

Пишет в
//home/market/production/mbi/reports/trust_transaction


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
Несколько дней



### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни

