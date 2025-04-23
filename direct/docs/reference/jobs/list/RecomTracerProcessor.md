## RecomTracerProcessor

### Продукт/подсистема

Рекомендации - подсказки в интерфейсе (например, "Увеличьте бюджет" или "Загрузите креативы <определенных> форматов").


### Роль в работе продукта/подсистемы

Есть рекомендации, которые рассчитываются в фоне и сохраняются в таблицу в YT, т.н. оффлайн-рекомендации. Изменения в базе могут привести к тому, что рассчитанная рекомендация окажется неактуальной. Джоба следит за изменениями бинлогов и отменяет рекомендации, если изменения потенциально могли привести к тому, что рекомендация стала неактуальной.


### Датафлоу

- ESS-процессор следит за изменениями в MySQL, которые потенциально могут влиять на отмену рекомендаций.
- Выбирает активные рекомендации для потенциальных изменений
- Для отмененных рекомендаций добавляет строку в таблицу [ppc.recommendations_status](https://direct-dev.yandex-team.ru/db/ppc/tables/recommendations_status.html). На сенеки обновленный статус приезжает [репликатором](../../../glossary/glossary.md#b2yt).


### Способы наблюдения за текущим состоянием

- [Общий дашборд ESS](https://solomon.yandex-team.ru/?project=direct&dashboard=ess&project=direct&cluster=app_binlogbroker&service=java-monitoring&env=production&b=2021-03-14T09%3A41%3A19.102Z&e=2021-03-15T09%3A41%3A19.102Z)
- [Отставание отмены рекомендаций по шардам](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.sensor=binlog_delay&l.shard=*&graph=auto&l.ess_processor=recom_tracer&stack=false&b=2021-03-14T09%3A44%3A07.822Z&e=2021-03-15T09%3A44%3A07.822Z)
- [Количество обработанных объектов по шардам](https://solomon.yandex-team.ru/?project=direct&cluster=app_java-jobs&service=java-monitoring&l.host=CLUSTER&l.sensor=logic_objects_count&l.shard=*&graph=auto&l.ess_processor=recom_tracer&transform=differentiate&b=2021-03-14T09%3A44%3A39.989Z&e=2021-03-15T09%3A44%3A39.989Z)
- [График отставания вычитки топика ESS-роутером](https://nda.ya.ru/t/oNKjvxjO3wuMGn)
- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.RecomTracerProcessor.working.production&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'recomtracer.RecomTracerProcessor)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Автоматическая отмена неактуальных рекомендаций, средняя критичность.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи могут заметить неактуальные рекомендации, например, рекомендацию увеличить бюджет, когда бюджет уже увеличен.


### Контакты разработчиков и менеджеров

Разработчики: [Марина Спиридонова](https://staff.yandex-team.ru/mspirit), [Игорь Костромин](https://staff.yandex-team.ru/elwood), [Лёша Кашицын](https://staff.yandex-team.ru/aliho)


### Желательное время исправления в случае поломки

В течение дня.


### Способы регулирования работы джобы

- [Общие способы регулирования работы ESS-процессоров](../jobs-common.md#control-ess)


### Известные причины поломок

- Проблемы с LogBroker, ESS.
- Проблемы с YT.
- Увеличение потока бинлогов может привести к отставанию.


### Дополнительно: тонкости и подводные камни
