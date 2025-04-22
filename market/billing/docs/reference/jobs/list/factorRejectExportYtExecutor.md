# factorRejectExportYtExecutor

### Код

Основной код:

[Job class - FactorRejectExportYtExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/factoring/services/FactorRejectExportYtExecutor.java)

[Service - FactorRejectExportYtService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/factoring/services/FactorRejectExportYtService.java)

[Dao - FactorRejectDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/factoring/dao/FactorRejectDao.java)

### Продукт/подсистема

Факторинг

### Роль в работе продукта/подсистемы

Джоба ежедневно выгружает в YT список клиентов, для последующего ручного определения,
кого банк-фактор(Альфа-Банк) не готов кредитовать.

### Датафлоу

Выгружаем все данные из таблицы `market_billing.factor_reject`
в таблицу в YT - `//home/market/production/billing/dictionaries/factoring/factor_reject`

### Способы наблюдения за текущим состоянием

- Juggler-мониторинг
- Логи
- Таблица в YT


### Какая функциональность пострадает от отказа джобы

Если джоба не будет работать, мы не сможем предоставить банк-фактору (Альфа-Банк) актуальный список клиентов
для которых нужно выполнить проверку.

### Как пользователи (или команда) заметят проблему и через какое время

Начнет гореть мониторинг (внутри `market-billing-tms-18`).

### Контакты разработчиков и менеджеров

Разработчики:
- [alex997](https://staff.yandex-team.ru/alex997)
- [k-sviridenko](https://staff.yandex-team.ru/k-sviridenko)

### Желательное время исправления в случае поломки

### Способы регулирования работы джобы

### Известные причины поломок
В данный момент не имеются.

### Дополнительно: тонкости и подводные камни
