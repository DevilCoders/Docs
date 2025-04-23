## SegmentStatusUpdateJob

### Продукт/подсистема

Сбор сегментов аудиторий ([подробнее](../../product/segments.md)).


### Роль в работе продукта/подсистемы

Актуализации статуса сегментов в базе Директа на основе статуса в Я.Адиториях.


### Датафлоу

Шардированная джоба.

- читает чанк записей с мета-информацией из таблицы [ppc.video_segment_goals](https://direct-dev.yandex-team.ru/db/ppc/tables/video_segment_goals.html)
- читает их статусы из таблицы в YT [//home/audience/production/export/segments_simple](https://yt.yandex-team.ru/hahn/navigation?path=//home/audience/production/export/segments_simple)
- обновляет статусы в [ppc.video_segment_goals](https://direct-dev.yandex-team.ru/db/ppc/tables/video_segment_goals.html) меньшими чанками

### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.SegmentStatusUpdateJob.working.production&project=direct.prod&query=&last=1DAY)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'status.SegmentStatusUpdateJob)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Сегменты, в которые недавно додились данные, зависнут в базе Директа в статусе "в обработке" и не будут дополняться новыми данными.


### Как пользователи (или команда) заметят проблему и через какое время

Пользователи примерно через сутки начнут замечать, что в Директе охват растет, а в Я.Аудиториях сегменты не увеличиваются.


### Контакты разработчиков и менеджеров

Разработчики: [Сергей Белоусов](https://staff.yandex-team.ru/mexicano)


### Желательное время исправления в случае поломки

Сутки.


### Способы регулирования работы джобы

Только константы в коде джобы.


### Известные причины поломок

- Проблема с сертификатами при доступе к YQL (от неё страдают все джобы, которые ходят в YQL).


### Дополнительно: тонкости и подводные камни
