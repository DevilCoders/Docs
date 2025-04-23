## OfflineAdvqKeywordsExportJob

### Продукт/подсистема

Прогноз показов по ключевым фразам.


### Роль в работе продукта/подсистемы

Выгружает для ADVQ все необходимые данные по ключевым фразам из неархивных кампаний для офлайн-прогноза показов по этим фразам.


### Датафлоу

- Данные для экспорта берутся из YT таблиц: [//home/direct/db/campaigns](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db/campaigns), [//home/direct/db/phrases](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db/phrases), [//home/direct/db/bids](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/db/bids).
- И записываются в таблицу [//home/direct/export/phrases_for_forecast](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/export/phrases_for_forecast) для последующей обработки.

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.OfflineAdvqKeywordsExportJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'export.OfflineAdvqKeywordsExportJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Основную пользовательскую функциональность джоба не затрагивает. Однако, при поломке перестанут обновляться прогнозы показов ключевых фраз.


### Как пользователи (или команда) заметят проблему и через какое время

Прогнозы показов ключевых фраз устареют и пользователям будут показываться неактуальные данные.


### Контакты разработчиков и менеджеров

Разработчики: [Александр Дуплищев](https://staff.yandex-team.ru/ppalex), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

В течение суток.


### Способы регулирования работы джобы

Отсутствуют.


### Известные причины поломок




### Дополнительно: тонкости и подводные камни

[Offline ADVQ на вики](https://wiki.yandex-team.ru/advq/offlineadvq/).
