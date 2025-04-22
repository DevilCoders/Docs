# scripts.moderateExportMaster.working

[Алерт в juggler](https://juggler.yandex-team.ru/check_details/?host=checks.direct.yandex.ru&service=scripts.moderateExportMaster.working&query=&last=1DAY).

## Описание { #description }
Скрипт совершает итерации работы (начинает и заканчивает) в своём шарде.

## Диагностика { #diagnostics }
Посмотреть логи скрипта, проверить нет ли зависших запросов в базе.

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [логи скрипта в логвьювере](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(service~'direct.script~method~'moderateExportMaster)~limit~100~offset~0~reverseOrder~false~showTraceIdRelated~false))$)
