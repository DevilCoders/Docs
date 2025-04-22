## ContentCategoriesOldTablesCleanerJob

### Продукт/подсистема

Подсистема разметки урлов категориями и жанрами контента, а также категориями BrandSafety.

Примеры использования:
- Таргетинг на категории контента в охватных кампаниях.
- BrandSafety (не показываем рекламу в неприемлемом контенте).


### Роль в работе продукта/подсистемы

Часть data-flow по разметке интернет-страниц (url) категориями контента. Удаляет старые таблицы в yt.


### Датафлоу

- Читает настройки из секции `content_categories/yacofast_data_collector/tables_cleaner` [app-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/app-production.conf) приложения Jobs.
- Собирает возраст папок в YT.
- Удаляет таблицы старше определённой даты.


### Способы наблюдения за текущим состоянием

- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'contentcategories.ContentCategoriesOldTablesCleanerJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)

### Какая функциональность пострадает от отказа джобы

Будут накапливаться данные в YT (`ContentCategoriesYacofastDataCollectorJob` + несколько выгрузок DataAPI из папки `content_categories`), рано или поздно квота закончится. От этого пострадает все что работает с YT.


### Как пользователи (или команда) заметят проблему и через какое время?

Закончится квота в yt.


### Контакты разработчиков и менеджеров

Разработчики: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor), [Саид Аммаев](https://staff.yandex-team.ru/ammsaid) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko), [Иван Мологин](https://staff.yandex-team.ru/chelu)


### Желательное время исправления в случае поломки

Неделя+.


### Способы регулирования работы джобы

Список таблиц для удаления и время хранения находится в секции `content_categories/yacofast_data_collector/tables_cleaner` [app-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/app-production.conf) приложения Jobs.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
