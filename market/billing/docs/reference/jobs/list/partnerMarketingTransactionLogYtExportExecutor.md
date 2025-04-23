# Экспорт транзакционного лога маркетинговых услуг в YT

### Код

Используем общую [джобу экспорта тлога](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/executor/TransactionLogYtExportExecutor.java),
на вход которой передается специально сконфигурированный инстанс сервиса [TransactionLogService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/service/TransactionLogService.java).
Специфичность в том, что передается маркетинговый DAO [PartnerMarketingTransactionLogDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/dao/PartnerMarketingTransactionLogDao.java)
и путь в YT.

### Продукт/подсистема

Биллинг маркетинговых услуг для 1P-поставщиков (БМУ).

### Роль в работе продукта/подсистемы

Экспортирует записи из транзакционного лога маркетинговых услуг в YT.

### Датафлоу

Читает данные из таблицы маркетингового тлога `market_billing.marketing_transaction_log` и складывает их в YT.


### Способы наблюдения за текущим состоянием
- Juggler-проверки:
- Мониторинги:

### Какая функциональность пострадает от отказа джобы

Результаты обилливания не будут отправлены в Баланс, не сможем выставить счета на оплату партнерам, потеряем деньги.

### Как пользователи (или команда) заметят проблему и через какое время

(Планируются мониторинги)

### Контакты разработчиков и менеджеров

Разработчики: [prof](https://staff.yandex-team.ru/prof) <br/>

### Желательное время исправления в случае поломки

Важно, чтобы первого числа каждого месяца все данные за предыдущий месяц были отправлены в Баланс до 13:00 по Москве.

### Способы регулирования работы джобы

На время переезда из Oracle в PG:
  - market.billing.tms.marketing_tlog.export.enabled - отвечает за сбор тлога в `market-billing-tms`;

### Известные причины поломок

Известных причин нет.

### Дополнительно: тонкости и подводные камни

