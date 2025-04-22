# factorRejectSberYtImportExecutor

### Код

Основной код:

[Job class - FactorRejectYtImportExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/factoring/services/FactorRejectYtImportExecutor.java)

[Service - FactorRejectYtImportService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/factoring/services/FactorRejectYtImportService.java)

[Dao - FactorRejectDao](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/billing/factoring/dao/FactorRejectDao.java)

### Продукт/подсистема

Факторинг

### Роль в работе продукта/подсистемы

Джоба ежедневно выгружает из YT список клиентов, которых проверил Сбербанк.

### Датафлоу
Выгружаем все данные из таблицы в YT - `//home/market/production/billing/dictionaries/factoring/factor_reject_sber_result`

Для каждого `rejected, fetched, sent_to_check` создаем новый период отказа
(либо, если уже есть открытый период, ничего не делаем) в таблице `market_billing.factor_reject`.
Для клиентов, у которых есть открытый период отказа, но не попавших
в список `rejected, fetched, sent_to_check`, закрываем период отказа (заполняем поле `end_reject_date`).


### Способы наблюдения за текущим состоянием

- Juggler-мониторинг
- Логи
- Таблица в YT
- Изменения таблицы `market_billing.factor_reject`

### Какая функциональность пострадает от отказа джобы

Если джоба не будет работать, мы не сможем получить актуальный список клиентов, которых проверил Альфа-Банк.

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
