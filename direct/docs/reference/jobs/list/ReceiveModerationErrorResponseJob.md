## ReceiveModerationErrorResponseJob

### Продукт/подсистема

Модерация в целом.


### Роль в работе продукта/подсистемы

Принимает сообщения из очереди ошибок. Логирует и зажигает алерт.


### Датафлоу

- Читает поток ошибок из Модерации из очереди LogBroker. Топик прописан в [common-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf) в секции `moderation_service/logbroker/error/topic`.
- В зависимости от кода ошибки меняет статус проверки в Juggler. Маппинг кода ошибки на статус прописан в [common-production.conf](https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs-internal/config/src/main/resources/common-production.conf) в секции `moderation_service/logbroker/error/code_levels`.



### Способы наблюдения за текущим состоянием

- [Juggler-проверка](https://juggler.yandex-team.ru/check_details/?host=checks_auto.direct.yandex.ru&service=jobs.ReceiveModerationErrorResponseJob.working.production&query=&last=1DAY)
- [Логи ошибок в ess-moderation](https://direct.yandex.ru/logviewer#~(logType~'ess_moderation~form~(fields~(~'log_time~'cid~'pid~'bid~'action~'source~'success~'data~'span_id)~conditions~(source~'error)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [Логи](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.jobs~method~'moderation.ReceiveModerationErrorResponseJob)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)


### Какая функциональность пострадает от отказа джобы

Перестанем видеть ошибки, получаемые от Модерации, можем что-то пропустить. В очереди будут накапливаться сообщения.


### Как пользователи (или команда) заметят проблему и через какое время

Никак, только мониторинг.


### Контакты разработчиков и менеджеров

Разработчики: [Денис Говорков](https://staff.yandex-team.ru/oxid), [Арнольд Таммемяги](https://staff.yandex-team.ru/aleran)


### Желательное время исправления в случае поломки

В течение дня.


### Способы регулирования работы джобы

Отсутствуют.


### Известные причины поломок

Модерация отправляет некорректные сообщения.


### Дополнительно: тонкости и подводные камни
