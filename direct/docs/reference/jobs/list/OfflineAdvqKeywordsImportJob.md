## OfflineAdvqKeywordsImportJob

**TODO: уточнить и дополнить**

### Продукт/подсистема

Прогноз показов по ключевым фразам.


### Роль в работе продукта/подсистемы

Последняя джоба из трёх в цепочке получения офлайн-прогноза по ключевым фразам:
- [OfflineAdvqKeywordsExportJob](OfflineAdvqKeywordsExportJob.md)
- [OfflineAdvqProcessingJob](OfflineAdvqProcessingJob.md)
- OfflineAdvqKeywordsImportJob

Импортирует в MySQL прогнозы по ключевым фразам, подготовленные предыдущей джобой в цепочке. В последствии, прогнозы отображаются в интерфейсе Директа, а также используются для рассчёта ставок.


### Датафлоу

- Берёт данные из [//home/direct/import/offline_advq](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/import/offline_advq).
- По ним обновляет прогнозы ключевых фраз в [ppc.bids](https://direct-dev.yandex-team.ru/db/ppc/tables/bids.html)
- Обновляет статусы и даты прогнозов у групп объявлений во [phrases](https://direct-dev.yandex-team.ru/db/ppc/tables/phrases.html).


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.OfflineAdvqKeywordsImportJob.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'dataimport.OfflineAdvqKeywordsImportJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Основную пользовательскую функциональность джоба не затрагивает. Однако, при поломке перестанут обновляться прогнозы показов ключевых фраз.


### Как пользователи (или команда) заметят проблему и через какое время

Прогнозы показов ключевых фраз устареют и пользователям будут показываться неактуальные данные.


### Контакты разработчиков и менеджеров

Разработчики: [Александр Дуплищев](https://staff.yandex-team.ru/ppalex), [Сергей Журавлёв](https://staff.yandex-team.ru/zhur)


### Желательное время исправления в случае поломки

В течение суток.


### Способы регулирования работы джобы

Настройки в коде:
- `YT_CHUNKS_MAX_SIZE` - размер чанка для вычитки из YT-репозитория (по умолчанию — 1 000 000).
- `TIME_WASTE_COEF` - коэффициент времени сна воркера, который обновляет данные в MySQL.
- `UPDATE_CHUNK_SIZE` - размер чанка для апдейта записей в MySQL.

### Известные причины поломок




### Дополнительно: тонкости и подводные камни

[Offline ADVQ на вики](https://wiki.yandex-team.ru/advq/offlineadvq/).
