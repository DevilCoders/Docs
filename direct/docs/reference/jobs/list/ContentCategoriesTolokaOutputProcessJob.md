## ContentCategoriesTolokaOutputProcessJob

### Продукт/подсистема

Подсистема разметки урлов категориями и жанрами контента, а также категориями BrandSafety.

Примеры использования:
- Таргетинг на категории контента в охватных кампаниях.
- BrandSafety (не показываем рекламу в неприемлемом контенте).


### Роль в работе продукта/подсистемы

Джоба подхватывает урлы, размеченные Толокой, и приводит их нужному формату перед тем как их подхватит джоба [ContentCategoriesYacofastDataCollectorJob](ContentCategoriesYacofastDataCollectorJob.md).


### Датафлоу

- Читает урлы из таблиц в YT в директории: [home/direct/export/content_categories/toloka/output](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/toloka/output).
- Выходная таблица кладется в директорию [home/direct/export/content_categories/toloka/processed_output](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/toloka/processed_output).

- Джоба работает только на `Hahn`.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ContentCategoriesTolokaOutputProcessJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'contentcategories.ContentCategoriesTolokaOutputProcessJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

- Таргетинг на категории: будет недокрут на тех страницах, которые не разметились.
- Brand Safety: можем начать показывать рекламу в неприемлемом контенте.


### Как пользователи (или команда) заметят проблему и через какое время

- Таргетинг на категории: клиенты могут заметить недокруты на новых страницах из-за неполноты разметки.
- Brand Safety: клиенты увидят в статистике, что мы показываем их рекламу в неприемлемом контенте.


### Контакты разработчиков и менеджеров

Разработчики: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor), [Саид Аммаев](https://staff.yandex-team.ru/ammsaid) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko), [Иван Мологин](https://staff.yandex-team.ru/chelu)


### Желательное время исправления в случае поломки

1-2 дня.


### Способы регулирования работы джобы




### Известные причины поломок

- Падение yql-скрипта.


### Дополнительно: тонкости и подводные камни
