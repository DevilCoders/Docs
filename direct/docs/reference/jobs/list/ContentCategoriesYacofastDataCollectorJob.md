## ContentCategoriesYacofastDataCollectorJob

### Продукт/подсистема

Подсистема разметки урлов категориями и жанрами контента, а также категориями BrandSafety.

Примеры использования:
- Таргетинг на категории контента в охватных кампаниях.
- BrandSafety (не показываем рекламу в неприемлемом контенте).


### Роль в работе продукта/подсистемы

Часть data-flow по разметке интернет-страниц (url) категориями контента. Поставляет данные в хранилище БК Yacofast.


### Датафлоу

- берет данные из нескольких таблиц в YT
- объединяет
- складывает в другую таблицу в YT


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ContentCategoriesYacofastDataCollectorJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'contentcategories.ContentCategoriesYacofastDataCollectorJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

- Таргетинг на категории: будет недокрут на тех страницах, которые не разметились.
- Brand Safety: можем начать показывать рекламу в неприемлемом контенте.


### Как пользователи (или команда) заметят проблему и через какое время?

- Таргетинг на категории: клиенты могут заметить недокруты на новых страницах из-за неполноты разметки.
- Brand Safety: клиенты увидят в статистике, что мы показываем их рекламу в неприемлемом контенте.


### Контакты разработчиков и менеджеров

Разработчики: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor), [Саид Аммаев](https://staff.yandex-team.ru/ammsaid) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko), [Иван Мологин](https://staff.yandex-team.ru/chelu)


### Желательное время исправления в случае поломки

1-2 дня.


### Способы регулирования работы джобы

Список таблиц-источников находится в секции `content_categories/yacofast_data_collector/source_folders` [app-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/app-production.conf) приложения Jobs.
В случае проблем с одним из них, есть вариант его отключить, но лучше перед этим проконсультироваться с ответственными.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
