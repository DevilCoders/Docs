## ContentCategoriesTolokaInputPrepareJob

### Продукт/подсистема

Подсистема разметки урлов категориями и жанрами контента, а также категориями BrandSafety.

Примеры использования:
- Таргетинг на категории контента в охватных кампаниях.
- BrandSafety (не показываем рекламу в неприемлемом контенте).


### Роль в работе продукта/подсистемы

Джоба подхватывает урлы, пришедшие из Каталогии, находит неразмеченные ранее и отправляет их на разметку Толокой.


### Датафлоу

- Читает урлы из таблиц в YT в директории: [home/direct/export/content_categories/raw_urls](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/raw_urls). У каждой таблицы свой таймстемп в названии, как и у таблиц на выходе. По ним джоба отфильтровывает ранее обработанные.
- Ранее размеченные урлы хранятся в [home/direct/export/content_categories/toloka/executed_projects_by_url](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/toloka/executed_projects_by_url). По ней отфильтровываются урлы, размеченные ранее и повторно попавшие в свежие таблицы.
- Разметка идет по нескольким группам категорий, для каждой из них есть своя директория в папке [home/direct/export/content_categories/toloka/input](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/toloka/input). Для каждой группы категорий отрабатывается скрипт и формирует на выходе в соответствующей директории таблицу с урлами.

- Джоба работает только на `Hahn`.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ContentCategoriesTolokaInputPrepareJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'contentcategories.ContentCategoriesTolokaInputPrepareJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


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

- Ppc-property `JOBS_CONTENT_CATEGORIES_TOLOKA_URLS_DAY_LIMIT` - лимит за день на суммарное число строк в сформированных таблицах, для каждой группы категорий. Либо дефолтное значение в [app-production.conf приложения jobs](https://a.yandex-team.ru/arc_vcs/direct/jobs/src/main/resources/app-production.conf) в поле `content_categories/toloka/url_day_limit`.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
