## CpmDefaultSegmentIntermediateTableRemoveJob

### Продукт/подсистема

Сбор сегментов аудиторий ([подробнее](../../product/segments.md)).


### Роль в работе продукта/подсистемы

Удаляет устаревшие промежуточные таблички, которые создаёт джоба [CpmDefaultSegmentIntermediateTableCreateJob](CpmDefaultSegmentIntermediateTableCreateJob.md).


### Датафлоу

Нешардированная джоба, не взаимодействует с MySQL.

Последовательно удаляет таблички из директории [//home/direct/segments/1d](https://yt.yandex-team.ru/hahn/navigation?path=//home/direct/segments/1d),
от даты устаревания в прошлое до момента, пока таблички не закончатся.


### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.CpmDefaultSegmentIntermediateTableRemoveJob.working.production&project=direct.prod&last=1DAY&query=)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'intermediate.CpmDefaultSegmentIntermediateTableRemoveJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Данные в YT будут копиться.


### Как пользователи (или команда) заметят проблему и через какое время

На пользователей напрямую не влияет.


### Контакты разработчиков и менеджеров

Разработчики: [Азат Хузин](https://staff.yandex-team.ru/khuzinazat)


### Желательное время исправления в случае поломки

Месяц.


### Способы регулирования работы джобы



### Известные причины поломок




### Дополнительно: тонкости и подводные камни
