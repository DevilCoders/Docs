## ContentCategoriesYangInputPrepareJob

### Продукт/подсистема

Подсистема разметки урлов категориями и жанрами контента, а также категориями BrandSafety.

Примеры использования:
- Таргетинг на категории контента в охватных кампаниях.
- BrandSafety (не показываем рекламу в неприемлемом контенте).


### Роль в работе продукта/подсистемы

Джоба подхватывает с разных сервисов размеченные урлы и отправляет их на проверку ассессорами в Янге.


### Датафлоу

- Читает урлы из таблиц в YT в директориях: [home/direct/export/content_categories/raw_urls](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/raw_urls) для Каталогии, [home/direct/export/content_categories/toloka/processed_output](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/toloka/processed_output) для Толоки и [home/direct/export/content_categories/yacofast_data](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/yacofast_data) объединенные.
- Проверка идет по нескольким группам категорий, для каждой из них есть своя директория в папке [//home/direct/export/content_categories/toloka/yang](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/toloka/yang). Для одной из групп формируется подвыборка и копируется в директории остальных групп категорий.

- Джоба работает только на `Hahn`.



### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ContentCategoriesYangInputPrepareJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'contentcategories.ContentCategoriesYangInputPrepareJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

- Остановится пополнение ханипотов [home/direct/export/content_categories/toloka/honeypots/honeypots](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/toloka/honeypots/honeypots). Влияет на качество разметки Толокой.
- Остановится мониторинг точности/полноты. Пополняется здесь [home/direct/export/content_categories/toloka/monitoring/precision_recall_monitoring](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/toloka/monitoring/precision_recall_monitoring)


### Как пользователи (или команда) заметят проблему и через какое время

- Не увеличивается таблица ханипотов [home/direct/export/content_categories/toloka/honeypots/honeypots](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/content_categories/toloka/honeypots/honeypots)
- [Дэшборд в DataLens](https://datalens.yandex-team.ru/iue7hed4f49md-precisionandrecall?state=5fa4e2fa434) (поменять даты) - начнут пропадать или проседать метрики.



### Контакты разработчиков и менеджеров

Разработчики: [Егор Иватько](https://staff.yandex-team.ru/ivatkoegor), [Саид Аммаев](https://staff.yandex-team.ru/ammsaid) <br/>
Менеджеры: [Алексей Александров](https://staff.yandex-team.ru/hrustyashko), [Иван Мологин](https://staff.yandex-team.ru/chelu)


### Желательное время исправления в случае поломки

1-2 дня.


### Способы регулирования работы джобы

- ppc_property `JOBS_CONTENT_CATEGORIES_YANG_INPUT_PREPARE_LAST_START` - таймстемп предыдущего запуска. Таблицы, модифицированные раньше этого таймстемпа в подвыборку не попадают.
- `JOBS_CONTENT_CATEGORIES_YANG_URLS_DAY_LIMIT` - дневной лимит урлов в подвыборках суммарно на все сервисы. Либо дефолтное значение в [app-production.conf приложения jobs](https://a.yandex-team.ru/arc_vcs/direct/jobs/src/main/resources/app-production.conf) в поле `content_categories/yang/url_day_limit`.


### Известные причины поломок

- Падение yql-скрипта.


### Дополнительно: тонкости и подводные камни
