## BsExportMobileContentJob

### Продукт/подсистема

Транспорт в БК.


### Роль в работе продукта/подсистемы

Доставляет инфрормацию о рекламируемых мобильных приложениях в БК.


### Датафлоу

При обновлении джобой [UpdateStoreContentJob](UpdateStoreContentJob.md) данных о приложении в [ppc.mobile_content](https://direct-dev.yandex-team.ru/db/ppc/tables/mobile_content.html) может быть сброшен статус синхронизации с БК (`statusBsSynced`). Джоба `BsExportMobileContentJob` подхватывает такие записи и экспортирует их в БК (http запросы в ручку).


### Способы наблюдения за текущим состоянием

- [График кол-ва отправленных записей](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs-push&service=push-monitoring&l.env=production&l.flow=bsExportMobileContent&l.sensor=items_sent_count&l.host=CLUSTER&graph=auto&b=1h&e=)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.BsExportMobileContentJob.working.production&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'job.BsExportMobileContentJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Пару лет не обновлялись иконки приложений, это заметили когда был ребрендинг Беру -> Маркет.Покупки.
Если совсем не будет работать, то вероятно не смогут запуститься показы созданных РМП кампаний.


### Как пользователи (или команда) заметят проблему и через какое время




### Контакты разработчиков и менеджеров

Разработчики: [Захар Зибаров](https://staff.yandex-team.ru/zakhar), [Паша Рябов](https://staff.yandex-team.ru/pavryabov)


### Желательное время исправления в случае поломки

Как можно скорее.


### Способы регулирования работы джобы

- Ваншот для сброса статуса синхронизации для переотправки [mobilecontent.MobileContentResetStatusBsSyncedOneshot](https://a.yandex-team.ru/arc/trunk/arcadia/direct/oneshot/src/main/java/ru/yandex/direct/oneshot/oneshots/mobilecontent/MobileContentResetStatusBsSyncedOneshot.kt).


### Известные причины поломок




### Дополнительно: тонкости и подводные камни
