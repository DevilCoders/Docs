# Сбор обилленных значений в транзакционный лог маркетинговых услуг

### Код

Используем общую [джобу сбора в тлог](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/executor/TransactionLogCollectionExecutor.java),
на вход которой передается сервис [PartnerMarketingTransactionLogCollectionService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/collection/PartnerMarketingTransactionLogCollectionService.java).

[Конфиг PartnerMarketingTransactionLogConfig](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/config/PartnerMarketingTransactionLogConfig.java).

DAO:
  - [PartnerMarketingTransactionLogDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/dao/PartnerMarketingTransactionLogDao.java)
  - [PartnerMarketingTransactionLogCollectionDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/tlog/collection/PartnerMarketingTransactionLogCollectionDao.java)

### Продукт/подсистема

Биллинг маркетинговых услуг для 1P-поставщиков (БМУ).

### Роль в работе продукта/подсистемы

Собирает результаты обилливания в транзакционный лог маркетинговых услуг.

### Датафлоу

Читает данные из 4 таблиц:
  - `market_billing.billed_marketing_campaign` - результаты обилливания маркетинговых кампаний с фиксированной механикой;
  - `market_billing.billed_promo_order_items` - результаты обилливания маркетинговых кампаний с компенсационной механикой;
  - `market_billing.billed_marketing_campaign_corr` - корректировки по маркетинговым кампаниям с фиксированной механикой;
  - `market_billing.billed_promo_order_items_corr` - корректировки для кампаний с компенсационной механикой.

Обрабатывает полученные данные, гененирует новые транзакции и складывает их в транзакционный лог маркетинговых услуг -
таблицу `market_billing.marketing_transaction_log`.


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
  - market.billing.tms.marketing_tlog.collect.enabled - отвечает за сбор тлога в `market-billing-tms`;

### Известные причины поломок

Известных причин нет.

### Дополнительно: тонкости и подводные камни

