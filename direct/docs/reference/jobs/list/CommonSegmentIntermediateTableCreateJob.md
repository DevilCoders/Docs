## CommonSegmentIntermediateTableCreateJob

### Продукт/подсистема

Сбор сегментов аудиторий ([подробнее](../../product/segments.md)).


### Роль в работе продукта/подсистемы

Из подневных chevent-логов Крутилки создаёт промежуточные таблицы меньшего размера, из которых читают джобы сбора сегментов.
Промежуточные таблицы нужны для оптимизации.


### Датафлоу

Нешардированная джоба, не взаимодействует с MySQL.

- находит самую свежую промежуточную табличку в директории [//home/direct/segments/common/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/segments/common/1d)
- со следующей за её датой ищет исходные таблички Крутилки в директории [//cooked_logs/bs-chevent-cooked-log/1d](https://yt.yandex-team.ru/hahn/navigation?path=//cooked_logs/bs-chevent-cooked-log/1d)
- для каждой найденной более свежей таблички последовательно создаёт соответствующую промежуточную табличку


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.CommonSegmentIntermediateTableCreateJob.working.production&project=direct.prod&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'intermediate.CommonSegmentIntermediateTableCreateJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Перестанут появляться исходные данные для работы джоб создания и сбора сегментов.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи примерно через сутки начнут замечать, что в Директе охват растет, а в Я.Аудиториях сегменты не увеличиваются.


### Контакты разработчиков и менеджеров

Разработчики: [Азат Хузин](https://staff.yandex-team.ru/khuzinazat)


### Желательное время исправления в случае поломки

Сутки.


### Способы регулирования работы джобы

ppc-property:
- `segment_jobs_intermediate_start_log_date` - задаёт дату, с которой необходимо создать таблички. Штатно используется для первого запуска, когда еще нет ни одной промежуточной таблички. Так же может быть использована в случае поломки, если нужно перегенерировать таблички.
- `segment_jobs_ignore_missed_days` - игнорировать пропущенные дни в исходных логах. Позволяет продолжить сбор сегментов, когда из-за поломки в Крутилке отсутствуют логи за какой-то день. Позже можно перегенерировать промежуточные таблички, сдвинуть даты назад в internal tools и пересобрать сегменты за отсутствующую дату.

### Известные причины поломок




### Дополнительно: тонкости и подводные камни
