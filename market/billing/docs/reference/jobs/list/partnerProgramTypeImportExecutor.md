# PartnerProgramTypeImportExecutor

### Код

Основной код:

[сервис PartnerProgramTypeImportService](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/partner/PartnerProgramTypeImportService.kt)

[класс PartnerProgramTypeImportExecutor](https://a.yandex-team.ru/arc_vcs/market/billing/market-billing-tms/src/main/java/ru/yandex/market/core/partner/PartnerProgramTypeImportExecutor.kt)

### Продукт/подсистема

Импорт типов продуктов партнёров из YT

### Роль в работе продукта/подсистемы

Джоба импортирует таблицу с информацией о программах партнеров из YT.

### Датафлоу

Джоба читает данные из кластера, указанного в проперти `market.billing.yt.partner_program_type.host`.

Путь до таблицы с возвратами: `mbi.yt.return.path=//home/market/production/checkouter/cdc/checkouter_main/return`

Путь до таблицы с позициями возвратов: `market.billing.yt.partner_program_type.path=//home/market/production/mbi/dictionaries/partner_program_type/latest`

В одной транзакции осуществляется чтение и вставка данных по типам продуктов для партнёров.

### Способы наблюдения за текущим состоянием
- Мониторинг Juggler

### Какая функциональность пострадает от отказа джобы

Не будут импортироваться типы продуктов партнёров из YT.

Это будет влиять на формирование отчётов по УМ.

### Как пользователи (или команда) заметят проблему и через какое время

По мониторингам

### Контакты разработчиков и менеджеров

Разработчики: [Группа продуктовой разработки Биллинга Маркета](https://staff.yandex-team.ru/departments/yandex_monetize_market_marketdev_business_billing_dev_dep62586/) <br/>

### Желательное время исправления в случае поломки

Сутки

### Способы регулирования работы джобы

Переменной `market.billing.import.yt.partner_program_type.enabled` можно управлять работой джобы.
Значение `true` - работа разрешена, `false` или отсутствует - работа запрещена.

Размер батча для записи в базу задаётся переменной `market.billing.import.yt.partner_program_type.batch_size`.
Если значение отсутствует, используется 5000.

### Известные причины поломок

### Дополнительно: тонкости и подводные камни

