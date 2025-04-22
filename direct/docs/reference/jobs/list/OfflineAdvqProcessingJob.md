## OfflineAdvqProcessingJob

### Продукт/подсистема

Прогноз показов по ключевым фразам.


### Роль в работе продукта/подсистемы

Вторая джоба из трёх в цепочке получения офлайн-прогноза по ключевым фразам:
- [OfflineAdvqKeywordsExportJob](OfflineAdvqKeywordsExportJob.md)
- OfflineAdvqProcessingJob
- [OfflineAdvqKeywordsImportJob](OfflineAdvqKeywordsImportJob.md)

Из сформированного внешним сервисом ADVQ прогноза по ключевым фразам подготавливает данные для импорта в MySQL - фильтрует лишнее и раскладывает в отдельные таблички на каждый шард.

Следующая джоба подхватывает эти данные и импортирует в MySQL.


### Датафлоу

- Берет данные из [//home/advq/advq/direct_export/forecast_results](https://yt.yandex-team.ru/hahn/navigation?path=//home/advq/advq/direct_export/forecast_results)
- Отсеивает прогнозы, изменившиеся на небольшой процент.
- Делит данные по шардам и раскладывает каждый шард в отдельную таблицу в директории [//home/direct/import/offline_advq/phrases_forecast](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/import/offline_advq/phrases_forecast)


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.OfflineAdvqProcessingJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'processing.OfflineAdvqProcessingJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Основную пользовательскую функциональность джоба не затрагивает. Однако, при поломке перестанут обновляться прогнозы показов ключевых фраз.


### Как пользователи (или команда) заметят проблему и через какое время

Прогнозы показов ключевых фраз устареют и пользователям будут показываться неактуальные данные.


### Контакты разработчиков и менеджеров

Разработчики: [Александр Дуплищев](https://staff.yandex-team.ru/ppalex), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

В течение суток.


### Способы регулирования работы джобы




### Известные причины поломок




### Дополнительно: тонкости и подводные камни

[Offline ADVQ на вики](https://wiki.yandex-team.ru/advq/offlineadvq/).
