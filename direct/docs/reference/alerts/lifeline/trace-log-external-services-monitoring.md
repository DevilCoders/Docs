# Алерты запросов во внешние сервисы lifeline_traceLogExternalService

[Алерт в solomon для api5](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogExternalService-direct.api5)

[Алерт в solomon для intapi](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogExternalService-direct.intapi)

[Алерт в solomon для canvas](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogExternalService-direct.canvas)

[Алерт в solomon для perl](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogExternalService-direct.web.perl)

[Алерт в solomon для резолверов graphql](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogExternalService-direct.web.grid)

[Алерт в solomon для остальных java ручек](https://solomon.yandex-team.ru/admin/projects/direct/alerts/lifeline_traceLogExternalService-direct.web.java)

## Описание { #description }

Алерты появления запросов во внешние сервисы.
Строится на основе трейс логов. Срабатывает при появлении хотя бы одного такого запроса.
Остается гореть в течение 24 часов после срабатывания.

Данный алерт позволяет инвентаризировать походы во внешние сервисы.
Если видно большое количество запросов, то стоит подумать о рефакторинге

## Диагностика { #diagnostics }
### Проверить, не выкладывался ли недавно релиз
1. В описании каждой алерта в juggler есть ссылка, перед которой написано **AppVersionUrl**, на график с изменением версий. [Пример алерта](https://juggler.yandex-team.ru/raw_events/?query=host%3Dlifeline_traceLogCpu-direct.web.grid%26service%3Dgrid.addAds)
   Также в описании алерта есть ссылка на график. Перед ссылкой написано **Url:**
   Сравнить два графика с выкладной релиза и проблемой в алерте.
3. Попробовать найти среди тикетов релиза те, которые могли задеть. Если релевантный тикет в релизе найден, то проверить необходимость похода во внешний сервис.
4. Если изменение ожидаемо, то включить ручку в исключения. [Пример конфига](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/has_problem/traceLogExternalService-direct.intapi.json) по сервису, куда добавлять исключения
5. Если тикет не найдет, то завести задачу на разбор в zbp.

### Другое
при низкой частоте использования, например, внутренние отчеты, возможно, что данная ручка не был добавлена в исключения конфига. Нужно добавить его в исключения.

## Ссылки { #links }
Какие ссылки могут быть полезны:
- [LogViewer тейсов с запросами во внешние сервисы](https://direct.yandex.ru/logviewer/#~(logType~'messages~form~(fields~(~'log_time~'host~'service~'method~'trace_id~'span_id~'prefix~'log_level~'class_name~'message)~conditions~(method~'*25TraceLogSystemMonitoringJob*25~message~'*25traceLogExternalServiceMonitoringDataProcessor*25)~limit~100~offset~0~reverseOrder~true~showTraceIdRelated~false))$)
- [Пример конфигурации алерта](https://a.yandex-team.ru/arc/trunk/arcadia/direct/solo/registered/alert/infra/lifeline/config/has_problem/traceLogExternalService-direct.intapi.json)
