## ImportSitelinksFromBnoJob

### Продукт/подсистема

Саджест сайтлинков при редактировании ТГО объявлений. Саджест сайтлинков в Универсальных Кампаниях (`campaigns.source = 'uac'`).


### Роль в работе продукта/подсистемы

Обновляет динамическую табличку [//home/direct/import/sitelinks/current](https://yt.yandex-team.ru/seneca-sas/navigation?offsetMode=key&path=//home/direct/import/sitelinks/current) на сенеках, из которой java-web выбирает информацию о сайтлинках для саджеста (ручка в приложении web `ad_generation/generate_sitelinks` (не graphql-мутация)). В саджесте содержится информация о страницах из всего интернета, не только связанные с текущим пользователем.


### Датафлоу

- Источник данных - [//home/shinyserp/qdsaas/sources/bno:docid_setprops](https://yt.yandex-team.ru/arnold/navigation?path=//home/shinyserp/qdsaas/sources/bno:docid_setprops).
- Делаем запрос в БНО (большой навигационный ответ) [importSitelinksFromBno.sql](https://a.yandex-team.ru/arc/trunk/arcadia/direct/jobs/src/main/resources/sitelinks/importSitelinksFromBno.sql) за данными сайтлинков.
- Создаем временную таблицу на arnold и заливаем в неё полученные данные.
- Отдельной merge операцией делаем табличку подходящей для конвертации в динамическую.
- Копируем созданную таблицу с arnold на все кластеры seneca через transfer-manager.
- Далее, каждую успешно скопированную таблицу делаем динамической и монтируем.
- Меняем симлинк `current` на новую таблицу.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ImportSitelinksFromBnoJob.working.production&last=1DAY).
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'sitelinks.ImportSitelinksFromBnoJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$).


### Какая функциональность пострадает от отказа джобы

Если джоба перестанет обновлять таблицу, то:
1. будут саджестится устаревшие сайтлинки - сайтлинк не соответствует реальной странице.
2. перестанем предлагать новые страницы.

Если джоба каким-либо образом испортит таблицу на кластерах seneca, ручка саджеста будет пятисотить.

Создание объявлений от этого не должно сломаться, но лучше проверить, так как к моменту происшествия это может измениться.


### Как пользователи (или команда) заметят проблему и через какое время?

Сайтлинки либо не будут саджеститься совсем, либо будут саджестится нерелевантные, из-за устаревшей таблицы.


### Контакты разработчиков и менеджеров

Разработчики: [Саша Дубов](https://staff.yandex-team.ru/a-dubov), [Слава Бобень](https://staff.yandex-team.ru/darkkeks) <br/>
Менеджеры: [Ксюша Аникеева](https://staff.yandex-team.ru/anyksenya) (Универсальные Кампании), [Дима Боголюбов](https://staff.yandex-team.ru/bogolyubov) (Автогенерация Данных)


### Желательное время исправления в случае поломки

- Если таблица не обновляется, то желательно починить в течение суток или в ближайший рабочий день.
- Если таблица сломалась, то нужно ASAP перевесить симлинк `current` на валидную табличку с данными.
- Если проблема не разовая, то нужно отключить джобу до починки и оставаться на старой таблице. Далее действуем по схеме "таблица не обновляется".


### Способы регулирования работы джобы

Ppc-property `import_sitelinks_from_bno_enabled` включает джобу.


### Известные причины поломок

- Ошибки transfer-manager при копировании таблицы - в логах будут ошибки запросов к апи transfer-manager.
- Недоступен arnold - в логах ошибки выполнения YQL запроса (копирования таблицы с arnold или удаления временной таблицы).
